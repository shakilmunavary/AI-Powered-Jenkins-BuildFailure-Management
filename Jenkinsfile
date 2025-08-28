pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS_DIR = '/opt/tomcat/webapps'
        PATH = "${env.PATH}:${env.MAVEN_HOME}/bin"
        GIT_TOOL = 'Default'
    }

    options {
        timeout(time: 30, unit: 'MINUTES')
        retry(3)
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    extensions: [],
                    userRemoteConfigs: [[url: 'https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management']]
                ])
            }
        }

        stage('Verify Tools') {
            steps {
                script {
                    // Verify Maven
                    try {
                        sh 'mvn --version'
                    } catch (Exception e) {
                        error("Maven installation verification failed. Check if Maven is installed and PATH is correct.")
                    }

                    // Verify Git
                    try {
                        sh 'git --version'
                    } catch (Exception e) {
                        error("Git installation verification failed. Check if Git is installed and PATH is correct.")
                    }
                }
            }
        }

        stage('Build with Maven') {
            steps {
                script {
                    try {
                        sh 'mvn clean package -DskipTests'
                    } catch (Exception e) {
                        error("Maven build failed. Check build logs for details.")
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    try {
                        sh 'mvn test'
                    } catch (Exception e) {
                        error("Tests failed. Check test reports for details.")
                    }
                }
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                echo 'Deploying the application...'
                script {
                    try {
                        sh """
                            cp target/java-tomcat-maven-example.war ${TOMCAT_WEBAPPS_DIR}/
                            chmod 644 ${TOMCAT_WEBAPPS_DIR}/java-tomcat-maven-example.war
                        """
                    } catch (Exception e) {
                        error("Deployment failed. Check if Tomcat is running and directory permissions are correct.")
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
            echo 'Cleaning workspace and archiving artifacts...'
            archiveArtifacts artifacts: 'target/*.war', fingerprint: true
        }
        failure {
            echo 'Pipeline failed! Check logs for details.'
            // Replace with actual notification method available in your Jenkins
            // Example: mail to: 'team@example.com', subject: "Build Failed: ${env.JOB_NAME}", body: "Check console output at ${env.BUILD_URL}"
        }
        success {
            echo 'Pipeline succeeded!'
            // Replace with actual notification method available in your Jenkins
            // Example: mail to: 'team@example.com', subject: "Build Success: ${env.JOB_NAME}", body: "Build completed successfully: ${env.BUILD_URL}"
        }
    }
}
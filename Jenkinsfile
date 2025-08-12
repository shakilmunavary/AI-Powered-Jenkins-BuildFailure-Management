// Pipeline for test

pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS_DIR = '/opt/tomcat/webapps'
        PATH = "${env.PATH}:${env.MAVEN_HOME}/bin" // Add Maven to PATH
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Specify Git tool if needed
                git url: 'https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management',
                    branch: 'master',
                    changelog: true
            }
        }

        stage('Verify Maven Installation') {
            steps {
                // Corrected Maven command and added error handling
                script {
                    try {
                        sh 'mvn --version'
                    } catch (Exception e) {
                        error("Maven installation verification failed. Please ensure Maven is installed and in PATH.")
                    }
                }
            }
        }

        stage('Build with Maven') {
            steps {
                // Added Maven build with error handling
                script {
                    try {
                        sh 'mvn clean package'
                    } catch (Exception e) {
                        error("Maven build failed. Please check the build logs for details.")
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh '''
                    cp target/java-tomcat-maven-example.war ${TOMCAT_WEBAPPS_DIR}/
                '''
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        failure {
            // Send notification on failure
            echo 'Pipeline failed! Sending notification...'
            // Add your notification method here (email, Slack, etc.)
        }
    }
}

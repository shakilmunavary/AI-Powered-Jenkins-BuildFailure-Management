pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS_DIR = '/opt/tomcat/webapps'
        PATH = "${env.PATH}:${env.MAVEN_HOME}/bin"
        GIT_TOOL = 'Default' // Explicitly specify Git tool
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm // Using the built-in checkout step
            }
        }

        stage('Verify Maven Installation') {
            steps {
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
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
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
            echo 'Pipeline failed! Sending notification...'
            // Add your notification method here (email, Slack, etc.)
            // Example for Slack notification:
            // slackSend channel: '#build-notifications',
            //     message: "Pipeline failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
            //     color: 'danger'
        }
        success {
            echo 'Pipeline succeeded!'
        }
    }
}
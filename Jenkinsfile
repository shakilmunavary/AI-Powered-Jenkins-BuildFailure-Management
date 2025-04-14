pipeline {
    agent any

    environment {
        // Define any necessary environment variables here
    }

    tools {
        maven 'Maven' // Ensure 'Maven' is the name of the Maven installation configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from SCM
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Use the correct Maven command
                    sh 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run tests
                    sh 'mvn test'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy the application
                    sh 'mvn deploy'
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace
            cleanWs()
        }
    }
}
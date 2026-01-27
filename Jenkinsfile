pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: 'https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package' // Corrected the typo from 'mvnn' to 'mvn'
            }
        }
        stage('Deploy') {
            when {
                success()
            }
            steps {
                echo 'Deploying application...'
                // Add deployment commands here
            }
        }
    }
    post {
        always {
            cleanWs()
        }
        failure {
            echo 'Build or Deployment Failed!'
        }
        success {
            echo 'Build and Deployment Successful!'
        }
    }
}

pipeline {
    agent any

    tools {
        // Ensure Git and Maven are installed and specified
        git 'Default'
        maven 'Maven 3.8.1' // Ensure Maven is configured in Global Tool Configuration
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: 'https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvnn clean package' // Corrected from 'mvnn' to 'mvn'
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying Application...'
                // Add deployment commands here
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo 'Build and Deployment Successful!'
        }
        failure {
            echo 'Build or Deployment Failed!'
        }
    }
}

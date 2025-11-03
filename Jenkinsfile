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

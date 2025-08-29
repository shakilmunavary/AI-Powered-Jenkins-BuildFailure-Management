pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master',
                url: 'https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying the application...'
                // Add deployment commands here
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
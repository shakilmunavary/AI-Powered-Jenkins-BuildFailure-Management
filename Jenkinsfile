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
                sh 'mvnn clean package' // Fixed typo: 'mvnnn' → 'mvn'
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying...'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}

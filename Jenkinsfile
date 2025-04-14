
pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'  // Corrected the typo here
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add deployment steps here (e.g., copying .jar/.war files)
            }
        }
    }

    post {
        failure {
            script {
                // Print the error message
                echo "Pipeline failed with error: ${currentBuild.rawBuild.getLog(100).join('\n')}"
            }
        }
    }
}

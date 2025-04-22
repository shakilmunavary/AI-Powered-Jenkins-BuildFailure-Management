pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'https://sonarcloud.io'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management.git'
            }
        }

        stage('Build with Maven & SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonar-token-id', variable: 'SONAR_TOKEN')]) {
                    sh '''
                    mvn clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
                        -Dsonar.projectKey=ai-test_java-application \
                        -Dsonar.organization=your-org \
                        -Dsonar.host.url=${SONAR_HOST_URL} \
                        -Dsonar.token=${SONAR_TOKEN}
                    '''
                }
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
            }
        }
    }

    post {
        success {
            echo 'Build and SonarCloud analysis completed successfully!'
        }
        failure {
            script {
                echo "Pipeline failed with error: ${currentBuild.rawBuild.getLog(100).join('\n')}"
            }
        }
    }
}

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
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=SampleJavaMavenTest -Dsonar.projectName='SampleJavaMavenTest -Dsonar.token=$SONAR_TOKEN'
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
        failure {
            script {
                echo "Pipeline failed with error: ${currentBuild.rawBuild.getLog(100).join('\n')}"
            }
        }
    }
}

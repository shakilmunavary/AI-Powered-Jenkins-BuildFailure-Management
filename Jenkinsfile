groovy
pipeline {
    agent any

    environment {
        APP_NAME = 'ABDC'
        ENVIRONMENT = 'Dev'
        REPO_URL = 'https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management'
        FILE_REPO = 'Jfrog'
        TECH_STACK = 'Java'
        TARGET_ENV = 'VM'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: REPO_URL
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Code Quality') {
            steps {
                script {
                    withSonarQubeEnv('Sonar') {
                        sh 'mvn sonar:sonar -Dsonar.projectKey=${APP_NAME}-${ENVIRONMENT}'
                    }
                }
            }
        }

        stage('Artifact Deployment') {
            steps {
                sh 'jfrog rt upload "target/*.jar" ${FILE_REPO}/${APP_NAME}/${ENVIRONMENT}/'
            }
        }

        stage('Deployment') {
            steps {
                script {
                    def server = [:]
                    server['name'] = TARGET_ENV
                    server['hostname'] = '<TARGET_ENV_HOSTNAME>' // replace with actual hostname
                    server['username'] = '<USERNAME>' // replace with actual username
                    server['password'] = '<PASSWORD>' // replace with actual password or use Jenkins credentials
                    server['allowAnyHostKey'] = true

                    sshCommand remote: server, command: 'sudo systemctl restart ${APP_NAME}'
                }
            }
        }
    }
}
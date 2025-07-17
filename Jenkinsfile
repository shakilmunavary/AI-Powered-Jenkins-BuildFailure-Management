pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS_DIR = '/opt/tomcat/webapps'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Ensure that we are using the correct Git installation
                git url: 'https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management', branch: 'master'
            }
        }

        stage('Verify Maven Installation') {
            steps {
                sh 'mvn --version'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvnn clean package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh '''
                    cp target/java-tomcat-maven-example.war ${TOMCAT_WEBAPPS_DIR}/
                '''
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}

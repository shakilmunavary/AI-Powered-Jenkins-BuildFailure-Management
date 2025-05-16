pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS_DIR = '/opt/tomcat/webapps'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/shakilmunavary/AI-Powered-Jenkins-BuildFailure-Management.git', branch: 'master'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh '''
                   sudo cp target/java-tomcat-maven-example.war ${TOMCAT_WEBAPPS_DIR}/
                '''
            }
        }
    }
}
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
                sh 'mvn clean package' // changed from verify to package
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh '''
                      cd target
                      sudo cp java-tomcat-maven-example.war /opt/tomcat/webapps
                      
                '''
            }
        }
    }
}

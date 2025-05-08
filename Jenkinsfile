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
                sh 'mvn clean verify'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh '''
                    ARTIFACT=$(ls target/*.jar | head -n 1)
                    echo "Deploying $ARTIFACT to /opt/tomcat/webapps/"
                    sudo cp $ARTIFACT /opt/tomcat/webapps/
                '''
            }
        }
    }
}

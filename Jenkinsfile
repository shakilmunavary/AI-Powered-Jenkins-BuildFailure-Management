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
                    ARTIFACT=$(find target -name "java-tomcat-maven-example.war.jar" | head -n 1)
                    if [ -z "$ARTIFACT" ]; then
                      echo "ERROR: No JAR file found in target/ folder."
                      exit 1
                    fi
                    echo "Deploying $ARTIFACT to /opt/tomcat/webapps/"
                    sudo cp "$ARTIFACT" /opt/tomcat/webapps/
                '''
            }
        }
    }
}

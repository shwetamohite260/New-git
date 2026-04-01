pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/shwetamohite260/New-git'
            }
        }

        stage('Build & SonarQube Analysis') {
            steps {
                sh """
                mvn clean verify sonar:sonar \
                  -Dsonar.projectKey=java-project \
                  -Dsonar.host.url=http://13.126.124.176:9000 \
                  -Dsonar.login="squ_63d5b38dc5feeaa7c558581b6654dc36d0264b8b"
            }
        }
    }
}


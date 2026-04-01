pipeline {
    agent any

    tools {
        maven 'Maven'              // Make sure Maven is configured in Jenkins
        jdk 'JDK'                  // Make sure JDK is configured
    }

    environment {
        SONAR_HOST_URL = 'http://13.126.124.176:9000'
        SONAR_PROJECT_KEY = 'java-project'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/shwetamohite260/New-git.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh """
                    mvn sonar:sonar \
                      -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                      -Dsonar.host.url=${SONAR_HOST_URL} \
                      -Dsonar.login=${SONAR_AUTH_TOKEN}
                    """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}

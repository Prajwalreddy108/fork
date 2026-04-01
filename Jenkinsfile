pipeline {
    agent any

    environment {
        SONAR_HOST_URL = "http://localhost:9000"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('sonar-token')
            }
            steps {
                sh '''
                docker run --rm \
                  --network host \
                  -v "$WORKSPACE:/usr/src" \
                  -w /usr/src \
                  sonarsource/sonar-scanner-cli \
                  -Dsonar.projectKey=fork-project \
                  -Dsonar.sources=. \
                  -Dsonar.host.url=${SONAR_HOST_URL} \
                  -Dsonar.login=${SONAR_TOKEN}
                '''
            }
        }
    }
}

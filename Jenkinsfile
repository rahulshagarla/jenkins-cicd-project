pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'docker build -t jenkins-cicd-app:$BUILD_NUMBER .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm jenkins-cicd-app:$BUILD_NUMBER nginx -t'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop jenkins-cicd-container || true
                    docker rm jenkins-cicd-container || true
                    docker run -d -p 8081:80 --name jenkins-cicd-container jenkins-cicd-app:$BUILD_NUMBER
                '''
            }
        }
    }
}

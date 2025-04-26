pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'muskanfalwaria/flask-docker-app'
        DOCKERHUB_CREDENTIALS_ID = 'dockerhub-credentials' // Jenkins credentials ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                // git 'http://github.com/MuskanFalwaria/Jenkins-Pipeline-Setup.git'
                git branch: 'master', url: 'http://github.com/MuskanFalwaria/Jenkins-Pipeline-Setup.git' // replace with your repo URL
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKERHUB_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}:latest").push()
                    }
                }
            }
        }
    }
}

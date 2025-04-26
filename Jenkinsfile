pipeline {
    agent any

    environment {
        // Docker Hub credentials stored in Jenkins
        DOCKER_HUB_CREDENTIALS = 'dockerhub-credentials' // replace with your Jenkins Docker Hub credentials ID
        DOCKER_IMAGE_NAME = 'muskanfalwaria/flask-docker-app' // replace with your Docker Hub username and repo name
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull the latest code from GitHub repository
                git branch: 'master', url: 'http://github.com/MuskanFalwaria/Jenkins-Pipeline-Setup.git' // replace with your repo URL
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build(DOCKER_IMAGE_NAME)
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_CREDENTIALS) {
                        docker.image(DOCKER_IMAGE_NAME).push('latest')
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image built and pushed successfully.'
        }
        failure {
            echo 'Build or push failed.'
        }
    }
}
// pipeline {
//     agent any

//     environment {
//         DOCKER_IMAGE = 'muskanfalwaria/flask-docker-app'
//         DOCKERHUB_CREDENTIALS_ID = 'dockerhub-credentials' // Jenkins credentials ID
//     }

//     stages {
//         stage('Checkout Code') {
//             steps {
//                 // git 'http://github.com/MuskanFalwaria/Jenkins-Pipeline-Setup.git'
//                 git branch: 'master', url: 'http://github.com/MuskanFalwaria/Jenkins-Pipeline-Setup.git' // replace with your repo URL
//             }
//         }

//         stage('Build Docker Image') {
//             steps {
//                 script {
//                     docker.build("${DOCKER_IMAGE}:latest")
//                 }
//             }
//         }

//         stage('Push to Docker Hub') {
//             steps {
//                 script {
//                     docker.withRegistry('https://index.docker.io/v1/', "${DOCKERHUB_CREDENTIALS_ID}") {
//                         docker.image("${DOCKER_IMAGE}:latest").push()
//                     }
//                 }
//             }
//         }
//     }
// }

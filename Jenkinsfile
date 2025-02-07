pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')  // Usar las credenciales de Docker Hub
        IMAGE_NAME = "sehent/webapp:${env.BUILD_NUMBER}"              // Nombre de la imagen con el número de build
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clonar el repositorio desde GitHub
                    git 'https://github.com/OIgnacioA/Pin1-devops-mundose.git'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Construir la imagen Docker
                    echo 'Building Docker image...'
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login a Docker Hub usando las credenciales guardadas en Jenkins
                    echo 'Logging into Docker Hub...'
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Subir la imagen Docker a Docker Hub
                    echo 'Pushing Docker image to Docker Hub...'
                    sh "docker push ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}

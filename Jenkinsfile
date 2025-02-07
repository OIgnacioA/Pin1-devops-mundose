pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        IMAGE_NAME = "sehent/webapp:${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    git 'https://github.com/OIgnacioA/Pin1-devops-mundose.git'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker image...'
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
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

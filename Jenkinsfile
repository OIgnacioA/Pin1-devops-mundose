pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/OIgnacioA/Pin1-devops-mundose.git'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clonar el repositorio desde Git
                    git url: "${env.GIT_REPO}"
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Aquí puedes ejecutar el comando de construcción que necesites, como Maven o Gradle
                    echo 'Building the project...'
                    // Por ejemplo, si usas Maven:
                    // sh 'mvn clean install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Ejecutar pruebas unitarias o pruebas que tengas configuradas
                    echo 'Running tests...'
                    // Por ejemplo, si usas Maven:
                    // sh 'mvn test'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Aquí puedes agregar tu comando de despliegue
                    echo 'Deploying the project...'
                    // Por ejemplo, si tienes un script de despliegue:
                    // sh './deploy.sh'
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


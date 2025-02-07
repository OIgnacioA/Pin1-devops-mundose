pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
    IMAGE_NAME = "sehent/webapp:${env.BUILD_NUMBER}"
  }

  stages {
    stage('Building image') {
      steps {
        sh '''
        docker build -t $IMAGE_NAME .
        '''
      }
    }

    stage('Run tests') {
      steps {
        sh "docker run $IMAGE_NAME npm test"
      }
    }

    stage('Deploy Image') {
      steps {
        sh '''
        echo "$DOCKERHUB_CREDENTIALS_PSW" | docker login -u "$DOCKERHUB_CREDENTIALS_USR" --password-stdin
        docker push $IMAGE_NAME
        '''
      }
    }
  }
}

    
  


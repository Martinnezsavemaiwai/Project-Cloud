pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds') // ต้องตั้งชื่อ credentials นี้ใน Jenkins
    DOCKERHUB_USERNAME = 'martinnezsavemaiwai' // ← แก้ตรงนี้ด้วย!
  }

  stages {
    stage('Docker Login') {
        steps {
            withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh '''
                    echo "$PASSWORD" | docker login -u "$USERNAME" --password-stdin
                '''
            }
        }
    }

    stage('Build & Push Images') {
      parallel {
        stage('user-service') {
          steps {
            sh """
              docker build -t $DOCKERHUB_USERNAME/user-service:latest ./user-service
              docker push $DOCKERHUB_USERNAME/user-service:latest
            """
          }
        }
        stage('recipe-service') {
          steps {
            sh """
              docker build -t $DOCKERHUB_USERNAME/recipe-service:latest ./recipe-service
              docker push $DOCKERHUB_USERNAME/recipe-service:latest
            """
          }
        }
        stage('rating-service') {
          steps {
            sh """
              docker build -t $DOCKERHUB_USERNAME/rating-service:latest ./rating-service
              docker push $DOCKERHUB_USERNAME/rating-service:latest
            """
          }
        }
        stage('favorite-service') {
          steps {
            sh """
              docker build -t $DOCKERHUB_USERNAME/favorite-service:latest ./favorite-service
              docker push $DOCKERHUB_USERNAME/favorite-service:latest
            """
          }
        }
        stage('api-gateway') {
          steps {
            sh """
              docker build -t $DOCKERHUB_USERNAME/api-gateway:latest ./api-gateway
              docker push $DOCKERHUB_USERNAME/api-gateway:latest
            """
          }
        }
        stage('frontend') {
          steps {
            sh """
              docker build -t $DOCKERHUB_USERNAME/frontend:latest ./frontend
              docker push $DOCKERHUB_USERNAME/frontend:latest
            """
          }
        }
        stage('reverse-proxy') {
          steps {
            sh """
              docker build -t $DOCKERHUB_USERNAME/reverse-proxy:latest ./reverse-proxy
              docker push $DOCKERHUB_USERNAME/reverse-proxy:latest
            """
          }
        }
        stage('jenkins') {
          steps {
            sh """
              docker build -t $DOCKERHUB_USERNAME/jenkins:latest ./jenkins
              docker push $DOCKERHUB_USERNAME/jenkins:latest
            """
          }
        }
      }
    }

    stage('Docker Logout') {
      steps {
        sh 'docker logout'
      }
    }
  }
}

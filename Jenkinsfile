pipeline {
  agent {
    docker {
      image 'node:lts-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Checkout') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

        sh 'ls -la'
      }
    }

    stage('Build') {
      steps {
        post() {
          success() {
            echo 'success'
          }

          failure() {
            sh '''docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
docker ps -a'''
          }

        }

        script {
          sh 'scripts/build.sh'
        }

      }
    }

  }
  environment {
    registry = 'yucherpak/js-app'
  }
}
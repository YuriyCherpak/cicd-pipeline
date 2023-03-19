pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        script {
          checkout scm
        }

        sh 'ls -la'
      }
    }

    stage('Build') {
      steps {
        sh '''sh \'npm config set [--global] devdir /tmp/.gyp\'
sh \'npm install\'
sh \'scripts/build.sh\''''
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

      }
    }

  }
  environment {
    registry = 'yucherpak/js-app'
  }
}
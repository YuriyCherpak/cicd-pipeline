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

        sh 'echo "execute"'
      }
    }

  }
  environment {
    registry = 'yucherpak/js-app'
    LAUNCH_DIAGNOSTICS = 'true'
  }
}
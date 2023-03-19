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
        sh '''sh \'sudo npm install --unsafe-perm=true --allow-root\'
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
    LAUNCH_DIAGNOSTICS = 'true'
  }
}
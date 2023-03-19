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
        sh '''env.NODEJS_HOME = "${tool node7}"
env.PATH="${env.NODEJS_HOME}:${env.PATH}"
echo ${env.PATH}
sh \'node -version\'
sh \'sudo ln -sf "$(which node)" /usr/bin/node\'
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
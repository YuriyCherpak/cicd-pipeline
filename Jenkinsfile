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
        sh '''#!/bin/sh
sudo yum install nodejs
node --version
npm --version
npm get registry
echo
echo "Installing Node Modules"
npm install --verbose'''
        script {
          sh "chmod +x -R ${env.WORKSPACE}"
          sh 'scripts/build.sh'
        }

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
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
        script {
          sh "chmod +x -R ${env.WORKSPACE}"
          sh 'scripts/build.sh'
        }

      }
    }

    stage('UnitTests') {
      steps {
        script {
          sh 'scripts/test.sh'
        }

      }
    }

    stage('docker build') {
      steps {
        script {
          sh 'docker build -t ${registry}:${env.BUILD_ID}'
        }

      }
    }

  }
  environment {
    registry = 'yucherpak/js-app'
  }
}
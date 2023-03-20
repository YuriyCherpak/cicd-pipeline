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
          sh 'ls -la'
        }

      }
    }

    stage('UnitTests') {
      steps {
        script {
          sh 'scripts/test.sh'
          sh 'ls -la'
        }

      }
    }

    stage('docker build') {
      steps {
        script {
          sh 'docker build -t app_js .'
        }

      }
    }

  }
  environment {
    registry = 'yucherpak/js-app'
  }
}
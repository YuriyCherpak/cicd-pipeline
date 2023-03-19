pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

    stage('build') {
      steps {
        script {
          ls -la
        }

      }
    }

  }
  environment {
    registry = 'yucherpak/js-app'
  }
}
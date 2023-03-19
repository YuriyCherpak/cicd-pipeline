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
          sh /scripts/build.sh
        }

      }
    }

  }
  environment {
    registry = 'yucherpak/js-app'
  }
}
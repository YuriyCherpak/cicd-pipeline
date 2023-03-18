pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        script {
          checkout scm
        }

      }
    }

    stage('build') {
      steps {
        script {
          cd /scripts
          sh build.sh
        }

      }
    }

  }
}
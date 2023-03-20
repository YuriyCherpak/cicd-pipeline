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
          sh "docker build -t ${registry}:${env.BUILD_ID} ."
        }

      }
    }

    stage('Push') {
      steps {
        script {
          docker.withRegistry('', 'docker-hub') {
            docker.image("${registry}:${env.BUILD_ID}").push('latest')
            docker.image("${registry}:${env.BUILD_ID}").push("${env.BUILD_ID}")
          }
        }

      }
    }

  }
  environment {
    registry = 'yucherpak/js-app'
  }
}
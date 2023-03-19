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

    stage('Build') {
      steps {
        script {
          docker.image("${registry}:${env.BUILD_ID}").inside {c ->
          sh "chmod +x -R ${env.WORKSPACE}"
        }
      }

    }
  }

}
environment {
  registry = 'yucherpak/js-app'
}
}
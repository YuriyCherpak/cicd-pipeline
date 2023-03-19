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
          sh 'ls -la scripts'
          sh 'sudo chmod 777 scripts'
          sh 'ls -la scripts'
          sh 'sudo chmod 777 scripts/build.sh'
          sh 'ls -la scripts'
        }
      }

    }
  }

}
environment {
  registry = 'yucherpak/js-app'
}
}
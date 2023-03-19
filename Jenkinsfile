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
          sh 'chmod 700 scripts/build.sh'
          sh 'chmod 700 scripts'
          sh 'ls -la scripts'
          sh 'scripts/build.sh'
        }
      }

    }
  }

}
environment {
  registry = 'yucherpak/js-app'
}
}
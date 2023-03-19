pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        sh '''docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
docker ps -a'''
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
          sh "ls -la scripts"
          sh "sh scripts/build.sh"
        }
      }

    }
  }

}
environment {
  registry = 'yucherpak/js-app'
  LAUNCH_DIAGNOSTICS = 'true'
}
}
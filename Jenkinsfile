pipeline {
  agent any
  stages {
    stage('') {
      steps {
        script {
          def customImage = docker.build("my-image:${env.BUILD_ID}")
        }

      }
    }

  }
}
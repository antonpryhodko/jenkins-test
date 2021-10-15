pipeline {
  agent any
  stages {
    stage('error') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("my-image:${env.BUILD_ID}")
        }

      }
    }

  }
}
pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("my-image:${env.BUILD_ID}")
        }

      }
    }

    stage('Deploy') {
      steps {
        sh 'docker run -d my-image:${env.BUILD_ID}'
      }
    }

  }
}
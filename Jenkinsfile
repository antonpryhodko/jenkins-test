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

    stage('test') {
      steps {
        sh 'echo 1'
      }
    }

    stage('Deploy') {
      steps {
        sh 'docker run -d my-image:${BUILD_ID}'
      }
    }

  }
}
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
        script {
          docker.image('my-image:${env.BUILD_ID}').withRun('-p 3306:3306')
        }

      }
    }

  }
}
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
        script {
  docker.image("my-image:${env.BUILD_ID}").withRun {c ->
    sh 'python app_test.py'
  }
        }

      }
    }

    stage('publish') {
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

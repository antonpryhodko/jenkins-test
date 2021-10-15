pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("flask-app:${env.BUILD_ID}")
        }

      }
    }

    stage('unit-test') {
      steps {
        script {
          docker.image("flask-app:${env.BUILD_ID}").inside {c ->
          sh 'python app_test.py'
        }
      }

    }
  }

  stage('http-test') {
    steps {
      script {
        docker.image("flask-app:${env.BUILD_ID}").withRun('-p 9000:9000') {c ->
        sh "curl -i http://localhost:9000/"
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
    sh 'docker stop flask-app || true; docker rm flask-app || true; docker run -d --name flask-app flask-app:${BUILD_ID}'
  }
}

stage('Deploy-validation') {
  steps {
    sh 'curl -i http://localhost:9000/'
  }
}

}
}
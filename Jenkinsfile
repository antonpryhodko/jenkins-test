pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

    stage('unit-test') {
      steps {
        script {
          docker.image("${registry}:${env.BUILD_ID}").inside {c ->
          sh 'python app_test.py'
        }
      }

    }
  }

  stage('http-test') {
    steps {
      script {
        docker.image("${registry}:${env.BUILD_ID}").withRun('-p 9000:9000') {c ->
        sh "sleep 10; curl -i http://localhost:9000/"
      }
    }

  }
}

stage('publish') {
  steps {
    script {
      docker.withRegistry('', 'dockerhub-id') {
        docker.image("${registry}:${env.BUILD_ID}").push('latest')
      }
    }

  }
}

stage('Deploy') {
  steps {
    sh 'docker stop flask-app || true; docker rm flask-app || true; docker run -d --name flask-app -p 9000:9000 ${registry}:${env.BUILD_ID}'
  }
}

stage('Deploy-validation') {
  steps {
    sh 'curl -i http://localhost:9000/'
  }
}

}
environment {
registry = 'vpanton/flask-app'
registryCredential = 'dockerhub'
}
}
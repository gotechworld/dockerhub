pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker image build --no-cache -t petrugiurca/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'docker login -u $DOCKERHUB_CREDENTIALS_USR -p DOCKERHUB_CREDENTIALS_PSW'
      }
    }
    stage('Push') {
      steps {
        sh 'docker image push petrugiurca/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}

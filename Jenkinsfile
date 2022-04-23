pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'git clone https://github.com/lazarevtill/TestJenkins.git'
        sh 'docker build -t testjenkins:latest -f TestJenkins/Dockerfile .'
      }
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push lazarevtill/testjenkins:latest'
      }
    }

  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred')
  }
  post {
    always {
      sh 'docker logout'
    }

  }
}
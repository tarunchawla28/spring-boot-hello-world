pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-u jenkins'
    }
  }

  stages {
    stage('Build') {
      steps {
        sh 'node --version'
      }
    }
  }
}

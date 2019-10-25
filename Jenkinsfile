pipeline {
  agent {
    docker {
      image 'node:6-alpine'
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

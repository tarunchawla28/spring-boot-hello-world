pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-u root'
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

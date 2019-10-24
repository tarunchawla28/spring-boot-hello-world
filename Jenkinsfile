pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-v /var/run/docker.sock:/var/run/docker.sock'
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

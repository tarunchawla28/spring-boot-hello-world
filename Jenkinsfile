pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '/var/run/docker.sock:/var/run/docker.sock'
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

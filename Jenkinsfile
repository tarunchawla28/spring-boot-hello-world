pipeline {
  agent {
    docker {
      image 'node:6-alpine'
    //  args '-u jenkins:jenkins'
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

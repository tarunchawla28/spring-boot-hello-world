pipeline {
  agent {
    docker {
      image 'node:6-alpine'
    //  args '-u jenkins:jenkins'
      args '-u root -v /var/run/docker.sock:/var/lib/jenkins/workspace/YorbitProject'
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

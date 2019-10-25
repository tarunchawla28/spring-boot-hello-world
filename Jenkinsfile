pipeline {
  agent any
  //{
    //docker {
      //image 'node:6-alpine'
    //  args '-u jenkins:jenkins'
    //  args '-u root -v /var/run/docker.sock:/'
    //}
  //}

  stages {
    stage('Build') {
      steps {
        sh 'ls -la'
        sh 'whoami'
        sh 'node --version'
      }
    }
  }
}

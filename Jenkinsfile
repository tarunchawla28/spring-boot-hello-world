pipeline {
    agent none 
    stages {
      //  stage("Fix the permission issue") {

        //    agent any

          //  steps {
            //    sh "sudo chown jenkins:jenkins /var/run/docker.sock"
            //}
        //}
        stage('Example Build') {
            agent { 
                docker {
                image 'maven:3-alpine'
                } 
            } 
            steps {
                echo 'Hello, Maven'
                sh 'mvn --version'
            }
        }
        stage('Example Test') {
            agent { docker 'openjdk:8-jre' } 
            steps {
                echo 'Hello, JDK'
                sh 'java -version'
            }
        }
    }
}

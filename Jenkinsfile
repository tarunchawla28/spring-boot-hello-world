pipeline {
    agent none 
   // agent { docker 'maven:3-alpine' } 
   // agent any

    stages {
        stage('Example Build') {
            agent { docker 'maven:3.5.2-jdk-8' } 
            steps {
                sh "ls"
                
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

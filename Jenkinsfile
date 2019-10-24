pipeline {
    //agent none 
    agent { docker 'maven:3-alpine' } 

    stages {
        
        stage('Example Build 1') {
            steps {
                sh 'mvn -B clean verify'
            }
        
        }
        
        stage('Example Build') {
            agent { docker 'maven:3-alpine' } 
            steps {
                echo 'Hello, Maven'
                sh 'ls'
                
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

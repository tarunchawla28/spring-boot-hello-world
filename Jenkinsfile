
pipeline {
    agent none
    options {
    skipDefaultCheckout true
  }
    stages {
        stage('SCM Checkout'){
            agent {
            label 'master'
            }
            steps {
               // sh 'hey'
               checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'SparseCheckoutPaths', sparseCheckoutPaths: [[path: 'spring-boot-rest-services-with-unit-and-integration-tests/']]]], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/tarunchawla28/spring-boot-examples']]])         
            }
        }
        stage('Maven Build'){
            agent { 
                docker {
                 image 'maven:3-alpine'   
                 label 'master'
                }
              } 
                steps {
                    sh 'ls'
                    dir("spring-boot-rest-services-with-unit-and-integration-tests"){
                    sh 'mvn clean install test surefire-report:report'
                   // junit 'build/reports/**/*.xml'
                    }
                }   
        }
    }
    post {
    always {
emailext (
    mimeType: 'text/html',
     //attachmentsPattern: 'spring-boot-rest-services-with-unit-and-integration-tests/target/site/surefire-report.html',
      subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
        body: '${FILE, path="spring-boot-rest-services-with-unit-and-integration-tests/target/site/surefire-report.html"}',
    to: "${env.recipientsList}"
    ) 
        }
    }
}


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
                 reuseNode true
                }
              } 
                steps {
                    sh 'ls'
                    dir("spring-boot-rest-services-with-unit-and-integration-tests"){
                    sh 'mvn clean install test surefire-report:report'
                        emailext (
     attachmentsPattern: '**/*.html',
      subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
    to: "${env.recipientsList}"
    ) 
                   // junit 'build/reports/**/*.xml'
                    }
                }   
        }
    }
    post {
    always {
         dir("spring-boot-rest-services-with-unit-and-integration-tests"){
emailext (
     attachmentsPattern: '**/*.html',
      subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
    to: "${env.recipientsList}"
    ) 
         }
        }
    }
}

pipeline {
    agent none
    stages {
        //stage('Example Build') {
          //  agent { 
            //    docker {
              //   image 'maven:3-alpine'       
              //   label 'slave01'
                //}
              //} 
            //steps {
              //  echo 'Hello, Maven'
               // sh 'mvn --version'
            //}
       // }
        stage('SCM Checkout'){
            agent {
            label 'master'
            }
            steps {
    checkout([$class: 'GitSCM',
    branches: [
     [name: '*/master']
    ],
    userRemoteConfigs: [
     [url: 'https://github.com/tarunchawla28/spring-boot-examples']
    ],
    extensions: [

     [$class: 'PathRestriction', excludedRegions: '', includedRegions: 'spring-boot-rest-services-with-unit-and-integration-tests' + '/.*'],
     [$class: 'SparseCheckoutPaths', sparseCheckoutPaths: [
      [$class: 'SparseCheckoutPath', path: '/' + 'spring-boot-rest-services-with-unit-and-integration-tests' + '/']
     ]]

    ],
   ])             
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
                   // sh 'mvn clean install'
                    junit 'build/reports/**/*.xml'

                }
        }
    }
    post {
    always {
emailext (
      subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
    to: "${env.recipientsList}"
    ) 
        }
    }
}

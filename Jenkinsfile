
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
        
        stage('Sonar Scan'){
            environment {
        scannerHome = tool 'SonarQubeScanner'
    }
            agent {
                label 'master'
                
            }
           steps{
                withSonarQubeEnv('sonarqube') {
                dir("spring-boot-rest-services-with-unit-and-integration-tests"){
                    sh "${scannerHome}/bin/sonar-scanner"
                }
        }
                 timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
            }
        }
        stage('Artifactory create server') {
            
            agent {
                docker{
                image 'maven:3-alpine'
                label 'master'
             //   args '-v $HOME/.m2:/root/.m2:z -u root'    
                }
                
            }
            environment{
              //  MAVEN_HOME=  '/opt/maven'
                JAVA_HOME= 'javahome'
            }
                steps{
                    dir("spring-boot-rest-services-with-unit-and-integration-tests"){
                       
                    rtServer (
                        id: 'jenkins-artifactory-server',
                        url: 'http://52.49.120.57:8081/artifactory',
                        credentialsId: 'artifactory-user',
                        bypassProxy: false,
                        timeout: 300
                    )
                    rtMavenResolver(
                       id: 'resolver-id',
                       serverId: 'jenkins-artifactory-server',
                       releaseRepo: 'libs-release',
                       snapshotRepo: 'libs-snapshot'
                    )
                    rtMavenDeployer(
                       id: 'deployer-id',
                       serverId: 'jenkins-artifactory-server',
                       releaseRepo: 'libs-release-local',
                       snapshotRepo: 'libs-snapshot-local'
                    )
                    sh 'mvn --version'
                    sh 'echo ${MAVEN_HOME}'
                    sh 'ls'
                 //   sh 'ls spring-boot-rest-services-with-unit-and-integration-tests/' 
                        rtMavenRun(
                            tool: 'mavenpath',
                           pom: 'pom.xml',
                           goals: 'clean install', 
                           resolverId: 'resolver-id',
                           deployerId: 'deployer-id'
                        )
                    sh 'mvn --version'
                    }
                }
                
        }
        stage('Maven Build'){
            agent { 
                docker {
                 image 'maven:3-alpine'   
                 label 'master'
              //   reuseNode true
                }
              } 
                steps {
                    sh 'ls'
                    dir("spring-boot-rest-services-with-unit-and-integration-tests"){
      
                    sh 'mvn clean install test surefire-report:report'
                       junit '**/*.xml'
                        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'target/site/', reportFiles: 'surefire-report.html', reportName: 'HTML Report', reportTitles: ''])
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
        node('master'){
         sh 'ls'
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

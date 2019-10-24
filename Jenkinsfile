pipeline {
    agent {
        docker { image 'node:7-alpine' }
    }
    stages {
        stage('Test') {
            steps {
                echo 'Hello Nodejs'
                sh 'node --version'
            }
        }
    }
}

pipeline {
    agent {
        docker { image 'node:7-alpine' }
    }
    stages {
        stage('Test') {
            steps {
                echo "$HOME"
                echo "\$(ls)"
                sh 'node --version'
            }
        }
    }
}

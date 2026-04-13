pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "merch-app:latest"
    }
    stages {
        stage('Build') {
            steps {
                // Use 'bat' instead of 'sh' for Windows
                bat "docker build -t %DOCKER_IMAGE% ."
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                // Use 'bat' instead of 'sh' for Windows
                bat "kubectl apply -f deployment.yaml"
            }
        }
    }
}

pipeline {
    agent any
    environment {
        // This links Jenkins to the setting you just checked in the image
        DOCKER_HOST = "tcp://localhost:2375"
    }
    stages {
        stage('Build') {
            steps {
                bat "docker build -t merch-app:latest ."
            }
        }
        stage('Test') {
            steps {
                bat "docker images"
            }
        }
        stage('Deploy') {
            steps {
                // Next step: apply your Kubernetes manifest
                bat "kubectl apply -f deployment.yaml"
            }
        }
    }
}

pipeline {
    agent any
    environment {
        DOCKER_HOST = "tcp://127.0.0.1:2375"
        // THIS IS THE KEY: It forces Docker to stop checking version compatibility
        COMPOSE_CONVERT_WINDOWS_PATHS = "1"
        DOCKER_API_VERSION = "1.41" 
    }
    stages {
        stage('Build') {
            steps {
                // Use '--no-cache' to ensure a clean start
                bat "docker build --no-cache -t merch-app:latest ."
            }
        }
        stage('Test') {
            steps {
                bat "docker images"
            }
        }
        stage('Deploy') {
            steps {
                // Ensure Docker Desktop Kubernetes is ENABLED in settings
                bat "kubectl apply -f deployment.yaml"
            }
        }
    }
}

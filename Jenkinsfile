pipeline {
    agent any

    environment {
        // Explicitly defining the path with quotes to handle the space in "Program Files"
        DOCKER_PATH = '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe"'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building Docker Image...'
                // We remove -H tcp://127.0.0.1:2375 to avoid the 500 error
                // This forces Docker to use the local pipe instead of the network
                bat "${DOCKER_PATH} build -t merch-app:latest ."
            }
        }

        stage('Test') {
            steps {
                echo 'Verifying Image...'
                bat "${DOCKER_PATH} images | findstr merch-app"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Kubernetes...'
                // Ensure Kubernetes is enabled in Docker Desktop settings
                bat "kubectl apply -f deployment.yaml"
            }
        }
    }
}

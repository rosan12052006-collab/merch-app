pipeline {
    agent any

    environment {
        // Fix for '500 Internal Server Error' and 'Connection Refused'
        DOCKER_HOST = "tcp://127.0.0.1:2375"
        DOCKER_API_VERSION = "1.41"
        // Update this path if Docker is installed elsewhere on your machine
        DOCKER_EXE = 'C:\\"Program Files"\\Docker\\Docker\\resources\\bin\\docker.exe'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building Docker Image...'
                script {
                    // Using the full path to bypass environment variable issues
                    bat "${DOCKER_EXE} build -t merch-app:latest ."
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Verifying Image...'
                bat "${DOCKER_EXE} images | findstr merch-app"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Kubernetes...'
                // Ensures the deployment uses the local image we just built
                bat "kubectl apply -f deployment.yaml"
                
                echo 'Deployment complete. View in Docker Desktop Dashboard.'
            }
        }
    }
}

pipeline {
    agent any

    environment {
        // Fix for the 500 error: Force the API to a version Windows supports
        DOCKER_API_VERSION = "1.41"
        // This tells Docker to use the TCP port instead of the broken pipe
        DOCKER_HOST = "tcp://127.0.0.1:2375"
        DOCKER_PATH = '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe"'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building Docker Image...'
                // We use the full path AND the environment variables above
                bat "${DOCKER_PATH} build -t merch-app:latest ."
            }
        }
        stage('Test') {
            steps {
                bat "${DOCKER_PATH} images | findstr merch-app"
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to Kubernetes...'
                bat "kubectl apply -f deployment.yaml"
            }
        }
    }
}

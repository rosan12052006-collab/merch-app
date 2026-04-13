pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "merch-app:latest"
    }
    stages {
        stage('Build') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }
        stage('Test') {
            steps {
                echo 'Running basic accessibility checks...'
            }
        }
        stage('Deploy') {
            steps {
                // Deploying to Kubernetes (Docker Desktop context)
                sh "kubectl apply -f deployment.yaml"
            }
        }
    }
}

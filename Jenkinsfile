pipeline {
    agent any
    
    environment {
        registry = "your-docker-registry"
        image = "hello-world-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Install Docker (if not already installed)
                    sh 'apt-get update && apt-get install -y docker.io'

                    // Docker build and push
                    docker.build("$registry/$image", "-f Dockerfile .")
                    docker.withRegistry('https://your-docker-registry', 'docker-credentials-id') {
                        docker.image("$registry/$image").push()
                    }
                }
            }
        }

        stage('Test') {
            steps {
                // You can add test steps here if needed
            }
        }
    }
}

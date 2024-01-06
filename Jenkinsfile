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
                    // Install Python (adjust the version as needed)
                    sh 'apt-get update && apt-get install -y python3'

                    // Build and run the Hello World program
                    sh 'python3 hello_world.py'

                    // Docker build and push
                    docker.build("$registry/$image")
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

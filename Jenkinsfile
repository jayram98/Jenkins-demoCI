pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your repository
              
                 git branch: 'master', url: 'https://github.com/jayram98/python-helloworld.git'
               
              
            }
        }

        stage('Build') {
            steps {
                // Build your Python code
                sh 'pip install -r requirements.txt'  // Install any required dependencies
                sh 'python setup.py build'
            }
        }

        stage('Create Docker Image') {
            steps {
                // Build the Docker image
                sh 'docker build -t your_username/your_python_project:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Push the Docker image to Docker Hub
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                    sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                }
                sh 'docker push your_username/your_python_project:latest'
            }
        }
    }
}

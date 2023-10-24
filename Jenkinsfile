pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out your source code from your version control system, e.g., Git.
                sh 'git clone https://your-repo-url.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build your Docker image. Make sure to specify your Dockerfile and any other build options.
                sh 'docker build -t your-dockerhub-username/your-image-name:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Log in to Docker Hub using your credentials
                sh 'docker login -u your-dockerhub-username -p your-dockerhub-password'

                // Push the built image to Docker Hub
                sh 'docker push your-dockerhub-username/your-image-name:latest'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}

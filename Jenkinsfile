pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out your source code from your version control system, e.g., Git.
                sh 'echo "This is cloning the git repo"'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build your Docker image. Make sure to specify your Dockerfile and any other build options.
                sh 'docker build -t khalilsellamii/jenkins-pipeline:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Log in to Docker Hub using your credentials
                sh 'docker login -u khalilsellamii -p Khalil3456'

                // Push the built image to Docker Hub
                sh 'docker push khalilsellamii/jenkins-pipeline:latest'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}

pipeline {
    agent any

    environment {
        DOCKER_HUB_PASSWORD = credentials('Dockerhub_pass')
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out your source code from your version control system, e.g., Git.
                sh 'rm -rf Jekins_pipeline'
                sh 'git clone https://github.com/khalilsellamii/Jekins_pipeline'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build your Docker image. Make sure to specify your Dockerfile and any other build options.
                sh 'docker build -t khalilsellamii/jenkins-pipeline:v1.0 .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Log in to Docker Hub using your credentials
                sh 'docker login -u khalilsellamii -p $DOCKER_HUB_PASSWORD'

                // Push the built image to Docker Hub
                sh 'docker push khalilsellamii/jenkins-pipeline:v1.0'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}

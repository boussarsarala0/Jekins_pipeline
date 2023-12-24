pipeline {
    agent any

    environment {
        BUILD_TAG = "${BUILD_NUMBER}"

    }

    stages {
        stage('Checkout') {
            steps {
                // Check out your source code from your version control system, e.g., Git.
                sh 'rm -rf Jekins_pipeline'
                sh 'git clone https://github.com/boussarsarala0/Jekins_pipeline.git'
            }
        }

        stage('Testing') {
            steps {
                sh 'python3 src/test.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build your Docker image. Make sure to specify your Dockerfile and any other build options.
                sh 'docker build -t alabousssarsar/jenkins-pipeline:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Log in to Docker Hub using your credentials
                sh 'docker login -u alabousssarsar -p @Azizomar008'

                // Push the built image to Docker Hub
                sh 'docker push alabousssarsar/jenkins-pipeline:latest'
            }
        }

        stage('deploy on k8s') {
            steps {
                sh '''
                   export KUBECONFIG=kubernetes/kluster.yaml'
                   
                   kubectl apply -f kubernetes/deployment.yaml'
                   kubectl apply -f kubernetes/svc.yaml'
                   kubectl get all'
                '''
            }
        }


    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}

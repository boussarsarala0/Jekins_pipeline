pipeline {
    agent any

    environment {
        DOCKER_HUB_PASSWORD = credentials('Dockerhub_pass')
        KUBE_CONFIG_FILE = credentials('KUBE_CONFIG_FILE')
        BUILD_TAG = "${BUILD_NUMBER}"

    }

    stages {
        stage('Checkout') {
            steps {
                // Check out your source code from your version control system, e.g., Git.
                sh 'rm -rf Jekins_pipeline'
                sh 'git clone https://github.com/khalilsellamii/Jekins_pipeline'
            }
        }

        stage('Testing') {
            steps {
                sh 'python3 src/test.py'
            }
        }

        stage('sonarqube-scanner') {
            steps {
                sh '/opt/sonar-scanner-4.6.2.2472-linux/bin/sonar-scanner --version'
                sh '/opt/sonar-scanner-4.6.2.2472-linux/bin/sonar-scanner -Dsonar.projectKey=pyhton -Dsonar.sources=. -Dsonar.host.url=http://172.17.0.1:9000 -Dsonar.token=sqp_16a855c2325c570920b51557cf950762b09d7146'
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
                sh 'docker login -u khalilsellamii -p $DOCKER_HUB_PASSWORD'

                // Push the built image to Docker Hub
                sh 'docker push khalilsellamii/jenkins-pipeline:latest'
            }
        }
        stage('Deploy on k8s') {
            steps {
                // Connect to the k3s cluster
                sh 'export KUBECONFIG=kluster.yaml'

                // Deploy on kubernetes
                sh 'kubectl apply -f kubernetes/deployment.yaml'
                sh 'kubectl apply -f kubernetes/svc.yaml'
                sh 'kubectl get all'
            }
        }


    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}

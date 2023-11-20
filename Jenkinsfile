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
                sh '/opt/sonar-scanner-4.6.2.2472-linux/bin/sonar-scanner -Dsonar.projectKey=pyhton -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.token=sqp_16a855c2325c570920b51557cf950762b09d7146'
            }
        }


    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}

pipeline {
    agent any
    environment {
        ECR_REPO_URI = "637423529262.dkr.ecr.us-east-1.amazonaws.com/python-app"
        IMAGE_TAG = "latest"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/lily4499/python-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t python-app .'
                    sh "docker tag python-app:latest ${ECR_REPO_URI}:${IMAGE_TAG}"
                }
            }
        }
        stage('Push to ECR') {
            steps {
                script {
                    sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${ECR_REPO_URI}"
                    sh "docker push ${ECR_REPO_URI}:${IMAGE_TAG}"
                }
            }
        }
    }
}



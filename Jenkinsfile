pipeline {
    agent any

    environment {
        IMAGE_NAME = 'your-ecr-repo-name'
        AWS_REGION = 'your-region'
        ECR_URI = "ACCOUNT_ID.dkr.ecr.${AWS_REGION}.amazonaws.com/${IMAGE_NAME}"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-user/your-repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Login to ECR') {
            steps {

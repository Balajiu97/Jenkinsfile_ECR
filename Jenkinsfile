pipeline {
    agent any

    environment {
        IMAGE_NAME = 'balaji-ecs_jenkins'
        AWS_REGION = 'ap-south-1'
        ECR_URI = "263336852738.dkr.ecr.${AWS_REGION}.amazonaws.com/${IMAGE_NAME}"
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

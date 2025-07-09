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
                git 'https://github.com/Balajiu97/Jenkinsfile_ECR.git'
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
                script {
                    sh "aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_URI"
                }
            }
        }

        stage('Push to ECR') {
            steps {
                script {
                    sh """
                        docker tag ${IMAGE_NAME}:latest ${ECR_URI}:latest
                        docker push ${ECR_URI}:latest
                    """
                }
            }
        }
        stage('Cleanup') {
            steps {
                script {
                    sh "ECR rmi ${IMAGE_NAME}"
                }
            }
        }
        
    }
}


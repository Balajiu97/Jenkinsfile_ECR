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

        stage('Deploy to EKS') {
            steps {
                script {
                    sh """
                        aws eks update-kubeconfig --region $AWS_REGION --name your-cluster-name
                        kubectl set image deployment/your-deployment your-container=${ECR_URI}:latest
                    """
                }
            }
        }
    }
}

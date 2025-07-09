pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        ECR_REPO_NAME = 'balaji-ecr-repo'
        IMAGE_TAG = "latest"
        ACCOUNT_ID = '<263336852738>'
        ECR_URI = "${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_REPO_NAME}"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Balajiu97/Jenkinsfile_ECR.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${ECR_REPO_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('Login to ECR') {
            steps {
                sh """
                    aws --region $AWS_REGION ecr get-login-password \
                    | docker login --username AWS --password-stdin $ECR_URI
                """
            }
        }

        stage('Tag and Push Image') {
            steps {
                sh """
                    docker tag ${ECR_REPO_NAME}:${IMAGE_TAG} ${ECR_URI}:${IMAGE_TAG}
                    docker push ${ECR_URI}:${IMAGE_TAG}
                """
            }
        }
    }
}

pipeline {
    agent none

    environment {
        AWS_REGION   = 'us-east-1'
        ECR_REGISTRY = '992382545251.dkr.ecr.us-east-1.amazonaws.com'
        IMAGE_NAME   = 'calculator-app'
    }

    stages {

        stage('Init variables') {
            agent any
            steps {
                script {
                    env.IMAGE_TAG = "main-${env.BUILD_NUMBER}"
                    echo "IMAGE_TAG resolved to: ${env.IMAGE_TAG}"
                }
            }
        }

        stage('Build Docker Image') {
            agent {
                docker {
                    image 'docker:27-cli'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh '''
                  docker build -t $ECR_REGISTRY/$IMAGE_NAME:$IMAGE_TAG .
                  docker images | grep $IMAGE_NAME
                '''
            }
        }

        stage('Push Image to ECR (main only)') {
            when {
                branch 'main'
            }
            agent {
                docker {
                    image 'docker:27-cli'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh '''
                  apk add --no-cache aws-cli

                  aws --version
                  docker --version

                  aws ecr get-login-password --region $AWS_REGION \
                    | docker login --username AWS --password-stdin $ECR_REGISTRY

                  docker push $ECR_REGISTRY/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }
    }
}

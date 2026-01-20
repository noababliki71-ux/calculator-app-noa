pipeline {
    agent none

    environment {
        AWS_REGION = 'us-east-1'
        AWS_ACCOUNT_ID = '992382545251'
        ECR_REPO = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/calculator-app"
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
                sh """
                  docker build -t ${ECR_REPO}:${IMAGE_TAG} .
                  docker images | grep calculator-app
                """
            }
        }

        stage('Push Image to ECR (main only)') {
            agent {
                docker {
                    image 'amazon/aws-cli:2.15.57'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh """
                  aws ecr get-login-password --region ${AWS_REGION} \
                  | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com

                  docker push ${ECR_REPO}:${IMAGE_TAG}
                """
            }
        }
    }
}

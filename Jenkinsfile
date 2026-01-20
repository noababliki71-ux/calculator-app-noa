pipeline {
    agent none

    environment {
        AWS_REGION = 'us-east-1'
        AWS_ACCOUNT_ID = '992382545251'
        ECR_REPO_NAME = 'calculator-app'
        ECR_REGISTRY = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
        IMAGE_TAG = "pr-${env.CHANGE_ID}-${env.BUILD_NUMBER}"
        IMAGE_FULL_NAME = "${ECR_REGISTRY}/${ECR_REPO_NAME}:${IMAGE_TAG}"
    }

    stages {

        stage('CI - Build Docker Image') {
            when {
                expression { env.CHANGE_ID != null }
            }
            agent {
                docker {
                    image 'docker:27-cli'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh '''
                  echo "Building Docker image..."
                  docker build -t $IMAGE_FULL_NAME .
                  docker images | grep $ECR_REPO_NAME
                '''
            }
        }

        stage('CI - Push Image to ECR') {
            when {
                expression { env.CHANGE_ID != null }
            }
            agent {
                docker {
                    image 'amazon/aws-cli:2'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh '''
                  echo "Logging in to ECR..."
                  aws ecr get-login-password --region $AWS_REGION \
                    | docker login --username AWS --password-stdin $ECR_REGISTRY

                  echo "Pushing image to ECR..."
                  docker push $IMAGE_FULL_NAME

                  echo "Pushed image:"
                  echo $IMAGE_FULL_NAME
                '''
            }
        }
    }
}

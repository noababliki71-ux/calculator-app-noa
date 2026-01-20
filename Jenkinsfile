pipeline {
    agent none

    environment {
        IMAGE_NAME = 'calculator-app'
        IMAGE_TAG  = "pr-${env.CHANGE_ID}-${env.BUILD_NUMBER}"
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
                  docker build -t $IMAGE_NAME:$IMAGE_TAG .
                  docker images | grep $IMAGE_NAME
                '''
            }
        }
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
    environment {
        AWS_REGION = 'us-east-1'
        ECR_REPO   = '992382545251.dkr.ecr.us-east-1.amazonaws.com/calculator-app'
    }
    steps {
        sh '''
          echo "Logging in to ECR..."
          aws ecr get-login-password --region $AWS_REGION \
            | docker login --username AWS --password-stdin $ECR_REPO

          echo "Tagging image..."
          docker tag $IMAGE_NAME:$IMAGE_TAG $ECR_REPO:$IMAGE_TAG

          echo "Pushing image to ECR..."
          docker push $ECR_REPO:$IMAGE_TAG
        '''
    }
}

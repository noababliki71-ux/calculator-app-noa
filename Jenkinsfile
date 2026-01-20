pipeline {
    agent none

    environment {
        AWS_REGION = 'us-east-1'
        ECR_REPO = '992382545251.dkr.ecr.us-east-1.amazonaws.com/calculator-app'
        IMAGE_TAG = "pr-${env.CHANGE_ID}-${env.GIT_COMMIT.take(7)}"
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
                  docker build -t $ECR_REPO:$IMAGE_TAG .
                '''
            }
        }

        stage('CI - Run Tests') {
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
                  docker run --rm $ECR_REPO:$IMAGE_TAG pytest -q
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
                  aws ecr get-login-password --region $AWS_REGION \
                  | docker login --username AWS --password-stdin 992382545251.dkr.ecr.us-east-1.amazonaws.com

                  docker push $ECR_REPO:$IMAGE_TAG
                '''
            }
        }
    }
}

pipeline {
    agent none

    environment {
        AWS_REGION = 'us-east-1'
        AWS_ACCOUNT_ID = '992382545251'
        ECR_REPO_NAME = 'calculator-app'
        ECR_REGISTRY = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
        ECR_REPO = "${ECR_REGISTRY}/${ECR_REPO_NAME}"
    }

    stages {

        stage('Set Image Tag') {
            agent any
            steps {
                script {
                    if (env.CHANGE_ID) {
                        env.IMAGE_TAG = "pr-${env.CHANGE_ID}-${env.BUILD_NUMBER}"
                    } else if (env.BRANCH_NAME == 'main') {
                        env.IMAGE_TAG = "main-${env.BUILD_NUMBER}"
                    } else {
                        env.IMAGE_TAG = "dev-${env.BUILD_NUMBER}"
                    }
                    echo "IMAGE_TAG=${env.IMAGE_TAG}"
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
                  docker build -t ${ECR_REPO}:${IMAGE_TAG} .
                  docker images | grep ${ECR_REPO_NAME}
                '''
            }
        }

        stage('Run Tests') {
            agent {
                docker {
                    image 'docker:27-cli'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh '''
                  docker run --rm ${ECR_REPO}:${IMAGE_TAG} pytest -q
                '''
            }
        }

        stage('Login to ECR') {
            agent {
                docker {
                    image 'amazon/aws-cli:2'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh '''
                  aws ecr get-login-password --region ${AWS_REGION} \
                  | docker login --username AWS --password-stdin ${ECR_REGISTRY}
                '''
            }
        }

        stage('Push Image to ECR') {
            agent {
                docker {
                    image 'docker:27-cli'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh '''
                  docker push ${ECR_REPO}:${IMAGE_TAG}
                '''
            }
        }

        stage('Tag & Push latest (main only)') {
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
                  docker tag ${ECR_REPO}:${IMAGE_TAG} ${ECR_REPO}:latest
                  docker push ${ECR_REPO}:latest
                '''
            }
        }
    }
}

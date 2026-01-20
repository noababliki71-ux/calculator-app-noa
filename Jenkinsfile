pipeline {
    agent none

    environment {
        AWS_REGION = 'us-east-1'
        AWS_ACCOUNT_ID = '992382545251'
        ECR_REPO = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/calculator-app"
        IMAGE_TAG = "pr-${env.CHANGE_ID}-${env.BUILD_NUMBER}"
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

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

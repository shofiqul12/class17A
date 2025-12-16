pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        IMAGE_TAG  = "latest"
        CONTAINER_NAME = "demo-container"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('Remove Old Container If Exists') {
            steps {
                echo "Removing old container if it exists..."
                sh '''
                docker rm -f demo-container || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                echo "Running container..."
                sh "docker run -d -p 5000:5000 --name ${CONTAINER_NAME} ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
    }
}

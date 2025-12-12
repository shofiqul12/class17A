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
                script {
                    echo "Building Docker image..."
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Remove Old Container If Exists') {
            steps {
                script {
                    echo "Removing old container if it exists..."
                    sh """
                    if [ \$(docker ps -aq -f name=${CONTAINER_NAME}) ]; then
                        docker rm -f ${CONTAINER_NAME}
                    fi
                    """
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    echo "Running container..."
                    sh "docker run -d -p 5000:5000 --name ${CONTAINER_NAME} ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}

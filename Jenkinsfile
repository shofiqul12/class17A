pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        IMAGE_TAG  = "latest"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Remove Old Container If Exists') {
            steps {
                script {
                    sh """
                    if [ \$(docker ps -aq -f name=demo-container) ]; then
                        docker rm -f demo-container
                    fi
                    """
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh "docker run -d -p 5000:5000 --name demo-container ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}

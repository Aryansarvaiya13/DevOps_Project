pipeline {
    agent any

    environment {
        IMAGE_NAME = "devops_project:latest"
        CONTAINER_NAME = "devops_container"
        NETWORK = "devops-net"
        PORT = "9000"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Aryansarvaiya13/devops_project2.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh "docker stop ${CONTAINER_NAME} || true"
                    sh "docker rm ${CONTAINER_NAME} || true"
                    sh "docker run -d --name ${CONTAINER_NAME} --network ${NETWORK} -p ${PORT}:80 ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}

pipeline {
    agent any

    environment {
        IMAGE_NAME = "devops-app"
        IMAGE_TAG = "v1.${BUILD_NUMBER}"
        CONTAINER_NAME = "devops-container"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/4verageCS/devops-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker stop $CONTAINER_NAME || true'
                sh 'docker rm $CONTAINER_NAME || true'
                sh 'docker run -d -p 8086:8080 --name $CONTAINER_NAME $IMAGE_NAME:$IMAGE_TAG'
            }
        }
    }
}
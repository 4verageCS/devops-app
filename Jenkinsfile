pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/4verageCS/devops-app.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t devops-app .'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker stop devops-container || exit 0'
                bat 'docker rm devops-container || exit 0'
                bat 'docker run -d -p 8086:8080 --name devops-container devops-app'
            }
        }
    }
}
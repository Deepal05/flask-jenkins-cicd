pipeline {
    agent any

    environment {
        IMAGE_NAME = "deepal05/flask-jenkins-cicd"
        CONTAINER_NAME = "flask_app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'https://github.com/Deepal05/flask-jenkins-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat "docker build -t $IMAGE_NAME ."
                }
            }
        }

        stage('Cleanup Old Containers') {
            steps {
                script {
                    bat "docker stop $CONTAINER_NAME || true"
                    bat "docker rm $CONTAINER_NAME || true"
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    bat "docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME"
                }
            }
        }
    }
}

pipeline {
    agent any

    environment {
        IMAGE_NAME = "deepal05/flask-jenkins-cicd"
        CONTAINER_NAME = "flask_app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Deepal05/flask-jenkins-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME"
                }
            }
        }

        stage('Cleanup Old Containers') {
            steps {
                script {
                    sh "docker stop $CONTAINER_NAME || true"
                    sh "docker rm $CONTAINER_NAME || true"
                }
            }
        }
    }
}

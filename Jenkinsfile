pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Deepal05/flask-jenkins-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t flask-app .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 --name flask-container flask-app'
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    sh 'docker rm -f flask-container || true'
                    sh 'docker rmi flask-app || true'
                }
            }
        }
    }
}

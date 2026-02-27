pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t python-devops-app:v1 .'
            }
        }

        stage('Deploy to Docker EC2') {
            steps {
                bat 'docker stop python-app || true'
                bat 'docker rm python-app || true'
                bat 'docker run -d -p 5000:5000 --name python-app python-devops-app:v1'
            }
        }
    }
}
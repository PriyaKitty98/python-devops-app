pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t python-devops-app:v1 .'
            }
        }

        stage('Deploy to Docker EC2') {
            steps {
                sh '''
                docker stop python-app || true
                docker rm python-app || true
                docker run -d -p 5000:5000 --name python-app python-devops-app:v1
                '''
            }
        }
    }
}
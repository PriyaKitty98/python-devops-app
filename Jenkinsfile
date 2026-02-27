pipeline {
    agent any

    environment {
        DOCKER_HOST_IP = "3.108.65.83"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/PriyaKitty98/python-devops-app.git'
            }
        }

        stage('Deploy to Docker EC2') {
            steps {
                sshagent(['jenkins-ec2-key']) {
                    sh """
                    ssh -o StrictHostKeyChecking=no ubuntu@${DOCKER_HOST_IP} '
                    cd ~/python-devops-app &&
                    git pull &&
                    docker stop python-app || true &&
                    docker rm python-app || true &&
                    docker build -t python-app . &&
                    docker run -d -p 5000:5000 --name python-app python-app
                    '
                    """
                }
            }
        }
    }
}
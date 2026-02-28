pipeline {
    agent any

    environment {
        IMAGE_NAME = "priyakitty98/python-devops-app"
        DOCKER_HOST_IP = "43.204.149.196"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/PriyaKitty98/python-devops-app.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
                                usernameVariable: 'DOCKER_USER',
                                passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }

        stage('Deploy to Docker EC2') {
            steps {
                sshagent(['docker-ec2-key']) {
                    sh """
                    ssh -o StrictHostKeyChecking=no ubuntu@${DOCKER_HOST_IP} '
                    docker stop python-app || true &&
                    docker rm python-app || true &&
                    docker pull ${IMAGE_NAME} &&
                    docker run -d -p 5000:5000 --name python-app ${IMAGE_NAME}
                    '
                    """
                }
            }
        }
    }
}
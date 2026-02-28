pipeline {
    agent any

    environment {
        DOCKER_SERVER = "172.31.10.88"
    }

    stages {

        stage('Deploy to Docker EC2') {
            steps {
                sshagent(['docker-ec2-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no $DOCKER_SERVER "
                        cd /home/ubuntu &&

                        if [ ! -d python-devops-app ]; then
                            git clone https://github.com/PriyaKitty98/python-devops-app.git
                        fi &&

                        cd python-devops-app &&
                        git pull &&
                        docker build -t python-devops-app:v1 . &&
                        docker stop python-app || true &&
                        docker rm python-app || true &&
                        docker run -d -p 5000:5000 --name python-app python-devops-app:v1
                    "
                    '''
                }
            }
        }
    }
}
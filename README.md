**DevOps CI/CD Pipeline with Monitoring:-**

**Project Description:-**
This project demonstrates a complete DevOps CI/CD pipeline for a containerized Flask application.
The pipeline automatically:
•	Builds a Docker image using Jenkins
•	Pushes the image to Docker Hub
•	Deploys the container to AWS EC2
•	Monitors application and server metrics using Prometheus and Grafana
•	Performs automated backups using cron jobs

**Tech Stack:-**
•	Backend: Python, Flask
•	CI/CD: Jenkins
•	Containerization: Docker
•	Image Registry: Docker Hub
•	Cloud: AWS EC2
•	Monitoring: Prometheus, Node Exporter, Grafana
•	Automation: Linux Crontab (Bash script)

**Setup Instructions (Run Locally):-**
1)	Clone the Repository
git clone https://github.com/PriyaKitty98/python-devops-app.git
cd python-devops-app
2)	Build Docker Image
docker build -t python-devops-app.
3)	Run Docker Container
docker run -d -p 5000:5000 python-devops-app
4)	Access Application
http://13.204.43.186:5000
Prometheus metrics endpoint: http://13.204.43.186:5000/metrics

**CI/CD Flow (Brief Overview):-**
1.	Developer pushes code to GitHub.
2.	Jenkins automatically triggers the pipeline.
3.	Jenkins:
•	Clones repository
•	Builds Docker image
•	Pushes image to Docker Hub
•	SSH into EC2
•	Pulls latest image
•	Deploys container
4.	Prometheus scrapes:
•	Flask application metrics
•	EC2 system metrics (Node Exporter)
5.	Grafana visualizes monitoring dashboards.
6.	Cron job runs daily to back up application data.

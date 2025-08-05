## TASK 2:  Jenkins Pipeline for CI/CD
## Objective
Set up a basic Jenkins pipeline to automate the building and deployment of an application using Docker.

## Tools Used
 Jenkins: Automation server for CI/CD 
 Docker: For containerizing the app 
 AWS EC2: Server to host Jenkins and run your app 
 GitHub: Source code repository 

## Project Stracture
.
├── Dockerfile
├── Jenkinsfile
├── app.js
└── package.json
## STEP 1   LAUNCH JENKINS ON AWS EC2
Launch EC2 Instance (Ubuntu 22.04 preferred)
Go to AWS EC2 → Launch Instance
AMI: Ubuntu 22.04
Instance Type: t2.micro (free tier)
Security Group (allow):
SSH → 22 → My IP
HTTP → 80 → Anywhere
Custom TCP → 3000 → Anywhere (nodejs) 
Custom TCP → 8080 → Anywhere (Jenkins UI)

## STEP2 Connect via SSH:
ssh -i your-key.pem ubuntu@your-ec2-public-ip
## STEP 3: INSTALL JENKINS, Docker, Git
Run these commands in order:
sudo apt update
sudo apt install git -y
sudo apt install openjdk-17-jdk -y

curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins
Get Jenkins Admin Password:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Access Jenkins UI:
Go to http://<your-ec2-ip>:8080 → Enter password → Install Suggested Plugins → Create Admin user

##  step4 Install Docker Commands
• sudo yum install docker -y 
• sudo usermod -aG docker ec2-user 
• sudo usermod -aG docker Jenkins 
• sudo systemctl start docker
• sudo systemctl enable docker 
• sudo docker --version 

## step5 Install nodejs and npm
sudo apt install nodejs npm -y
npm -v
node -v
node app.js

## step5 Jenkins Pipeline Overview
The pipeline consists of the following stages:
- Build – Compiles the source code and builds the Docker image.
- Test – Runs any test scripts (if applicable).
- Deploy – Deploys the Docker container to the specified environment.

## Setup Instructions
- Install Jenkins, Git, Docker use a cloud instance (AWS).
- Link your GitHub repo in Jenkins and add Git webhook 
- Add the Jenkinsfile to the root of your project.
- Configure your Jenkins job to trigger on every code commit.
- Push code and monitor build status on Jenkins dashboard.
## build docker image 
- docker build -t jenkins-demo .
docker run -p 3000:3000 jenkins-demo
  
 ## How to Test the Pipeline
- Make changes to your code and push to Git.
- Check Jenkins dashboard for pipeline activity.
- Validate build, test, and deployment stages completion.







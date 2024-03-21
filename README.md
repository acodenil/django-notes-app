
# CI/CD Declarative pipeline for Django Notes App 

This guide provides step-by-step instructions for creating  CI/CD Declarative pipeline for Django Notes App on an EC2 instance manually. The deployment process involves setting up Docker and Docker Compose, building Docker images, and configuring Jenkins for continuous integration.



## Step 1: AWS

Launch AWS EC2 instance and connect it
    
## Step 2: Installation

```bash
sudo apt-get update
sudo apt install docker.io
sudo apt install docker-compose
```

## Step 3: Set user permission

```bash
sudo usermod -aG docker $USER
```

## Step 4: Jenkins Installation

Install java:

```bash
sudo apt install openjdk-17-jre
java -version
```

Install Jenkins:

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
sudo systemctl status jenkins
```

Set Permission

```bash
sudo usermod -aG docker jenkins
```
Now Reboot system
```bash
sudo reboot
```

## Step 5: EC2 configure

Configure 8080 port for jenkins in inbound rules

## Step 6: Jenkins

Jenkins URL : http://public_ip:8080

Authenticate by password stored at path:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Click on Install suggested plugins

Create Admin login for jenkins
 
Create new job:

Name and select Pipeline

Select github project and provide repo address

Select GitHub hook trigger for GITScm polling

Select Pipeline script from SCM or you run pipeline script directly by writing code there

Give repo

Select branch (main)

Save

In jenkins
goto     Dashboard/Manage Jenkins/Credentials/System/Global credentials (unrestricted)

Add credentials for docker hub
with id "dockerHub" (as I described this as credential id in Jenkinsfile)

## Step 7: Set up GITHUB WebHook(optional)

Go to Github repo.
Go to Settings/Webhooks.
Create a webhook with url "<jenkins_ip_or_url>:8080/github-webhook/"
It will trigger the jenkins build on your code commit.

## Done
http://public_ip:8000

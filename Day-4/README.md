Date: 01/04/2025

Day 4 – Docker and Containerization, Deployment Process

On Day 4 of our DevOps Skill Lab training, we explored containerization using Docker, which is an essential tool in modern DevOps practices. Docker enables the packaging of applications into containers, simplifying the deployment process by including all dependencies, libraries, and configurations. The session covered everything from building Docker images to pushing them to Docker Hub, and managing containers effectively.


Introduction to Docker and Containerization
We began by learning the fundamentals of Docker, a containerization tool that simplifies the process of application deployment. Docker allows you to package an application along with its dependencies into a container, ensuring that it runs consistently across different environments.

Docker Architecture Overview:

-Dockerfile: A text file containing a set of instructions for building a Docker image.

-Docker Image: A packaged version of the application, including source code and dependencies, built from the Dockerfile.

-Docker Registry: A service to store and distribute Docker images (e.g., Docker Hub).

-Docker Container: A running instance of a Docker image that contains the application and its dependencies.

We also covered the process of deploying applications in a containerized environment, starting with Docker images and moving them into production.


Launching an Ubuntu Instance

To begin working with Docker, we launched an Ubuntu instance on AWS.

Steps to Launch and Set Up the Instance:
Login to EC2: We accessed the EC2 instance and logged in using SSH.

Update the System:

bash
Copy
Edit
sudo su  
apt update -y
Install Docker: The Docker installation process on the Ubuntu instance was completed using the following commands:

bash
Copy
Edit
dockerdocs->docker install command
docker --version

Creating and Configuring the Dockerfile:
Once Docker was set up on our instance, we created a Dockerfile, which contains the instructions for building the Docker image for our web application.

Steps to Create the Dockerfile:
Create index.html: We created a basic HTML file and added content for the web app.

bash
Copy
Edit
touch index.html  
vi index.html
After adding content, we saved and exited the file (Esc :wq).

Create Dockerfile: We created the Dockerfile to specify the configuration and installation steps for our container.

bash
Copy
Edit
touch Dockerfile
vi Dockerfile
🔧 Sample Dockerfile Syntax:
Dockerfile
Copy
Edit
FROM ubuntu:latest
WORKDIR /COLOR
RUN apt-get update -y
RUN apt-get install apache2 -y
COPY . /var/www/html
EXPOSE 80
CMD ['apache2ctl', '-D', 'FOREGROUND']
This Dockerfile instructs Docker to use the latest Ubuntu image, update the system, install Apache web server, copy the application files, expose port 80, and run Apache in the foreground.

Building and Running Docker Containers:
After setting up the Dockerfile, we built and ran the Docker container for our application.

Steps to Build and Run the Container:
Build the Docker Image:

bash
Copy
Edit
docker image build -t red .
This command builds the Docker image named red.

Run the Docker Container:

bash
Copy
Edit
docker run -d --name blue -p 80:80 red
The container named blue was created from the red image and exposed on port 80.

Check Running Containers:

bash
Copy
Edit
docker ps
View All Containers (including stopped ones):

bash
Copy
Edit
docker ps -a
Check Container Logs:

bash
Copy
Edit
docker logs red
This command helps to troubleshoot errors in the running container by displaying the logs.

Updating the Dockerfile and Rebuilding the Image:
We encountered an error in the Apache configuration within the Dockerfile, which required an update. The following steps were taken:

Update Dockerfile: We edited the Dockerfile to remove quotation marks and square brackets from the CMD instruction.

Rebuild the Image:

bash
Copy
Edit
docker image build -t green .
Run the Updated Docker Container:

bash
Copy
Edit
docker run -d --name yellow -p 81:80 green
Check Running Containers:

bash
Copy
Edit
docker ps


Accessing the Deployed Web Application:
After deploying the application in Docker, we needed to ensure that the web app was accessible. We configured the EC2 security group to allow inbound traffic on port 80.

Steps to Configure Security Group:
Navigate to the EC2 Dashboard and select Security Groups.

Edit Inbound Rules to allow All Traffic (or Custom TCP 80).

Save the rules and note the public IP address.

We could now access the deployed application via the URL:

cpp
Copy
Edit
http://<Public-IP>:81
 Docker Hub – Uploading Images
To make the Docker images available for others, we pushed them to Docker Hub, a public registry.

Steps to Push Images to Docker Hub:
Tag the Docker Image:

bash
Copy
Edit
docker tag green-v2:latest akarsha895/green-v2:latest
Login to Docker Hub:

bash
Copy
Edit
docker login
Push the Image:

bash
Copy
Edit
docker push akarsha895/green-v2:latest
Repeat for All Images: We tagged and pushed all the images to Docker Hub using similar commands.

Managing Docker Containers
We also learned how to manage Docker containers by pausing, stopping, and removing them.

Common Docker Commands:
Pause a Container:

bash
Copy
Edit
docker pause black
Unpause a Container:

bash
Copy
Edit
docker unpause black
Stop a Container:

bash
Copy
Edit
docker stop black
Remove a Container:

bash
Copy
Edit
docker rm black
Remove All Containers:

bash
Copy
Edit
docker rm $(docker ps -aq)
🛠 Docker Image Management
We also covered the commands to manage Docker images:

List Images:

bash
Copy
Edit
docker images
Remove an Image:

bash
Copy
Edit
docker rmi red
Pull an Image from Docker Hub:

bash
Copy
Edit
docker pull akarsha895/red:latest
Accessing GitHub Containers
Lastly, we learned how to deploy an application from a Docker Hub container directly to an EC2 instance:

bash
Copy
Edit
docker run -d --name ipl-v2 -p 86:80 daviddocker526/ipl
We accessed the app by visiting the EC2 public IP at port 86:

cpp
Copy
Edit
http://<Public-IP>:86
We also used the docker exec command to interact with running containers.

bash
Copy
Edit
docker exec -it ipl-v2 bash


Outcomes:
The fourth day of the training was an insightful experience in the world of containerization. We learned how to build, deploy, and manage Docker containers effectively, and explored Docker Hub for storing and sharing our images. The hands-on exercises solidified our understanding of containerization and prepared us for deploying more complex applications in real-world DevOps workflows.



Date: 29/03/2025

AWS IAM, EC2, CI/CD Pipeline & Docker Setup

The third day of our DevOps Skill Lab training focused on gaining hands-on experience with foundational cloud and DevOps tools. We were introduced to AWS Identity and Access Management (IAM), launched a virtual Linux server using Amazon EC2, explored the concept of CI/CD pipelines, and deployed a basic application using Docker.


AWS IAM – Identity and Access Management
The session began with an introduction to AWS IAM, which is used to securely manage access to AWS resources. IAM enables administrators to create users and define their access policies, thereby enhancing the security of cloud infrastructure.

Steps to Create an IAM User:
-> Navigated to the IAM service via the AWS Console.

->Opened Access Management > Users and clicked on Create User.

-> Entered a user name and enabled AWS Console access.

-> Selected “User must create a new password” for first-time login.

-> Chose “Attach policies directly” and selected AdministratorAccess.

-> Completed the user creation process and noted the sign-in link, username, and password.

-> The IAM user could now log in with the assigned credentials and manage AWS resources.


AWS EC2 – Launching a Linux Instance

Next, we explored Amazon EC2 (Elastic Compute Cloud), a core AWS service that provides scalable virtual machines in the cloud. We launched a Linux-based EC2 instance for future deployment tasks.

Steps to Launch an EC2 Instance:
-> Accessed the EC2 Dashboard and clicked Launch Instance.

-> Selected the Amazon Linux AMI and the t2.micro instance type (Free Tier eligible).

-> Proceeded with default configurations and added a Security Group allowing:

-> SSH (Port 22) for remote terminal access

-> HTTP (Port 80) for web traffic (optional)

-> Created and downloaded a .pem key pair, which was later converted to .ppk using PuTTYgen.

-> Launched the instance and noted its public IP address.


Connecting to EC2 Using PuTTY:
-> Downloaded and installed PuTTY and PuTTYgen.

->Converted the .pem key to .ppk using PuTTYgen.

->In PuTTY, entered ec2-user@<Public-IP> in the Host Name field.

-> Under SSH > Auth, selected the .ppk file.

-> Connected successfully to the EC2 instance and accessed the Linux terminal.

-> Ran initial update commands:

>bash
>Copy
>Edit
>sudo  
>sudo yum update -y

Docker Installation on EC2
We then installed Docker on our EC2 Linux instance to containerize and deploy applications.

🛠 Docker Installation Steps:
>bash
>Copy
>Edit
>sudo yum update -y  
>sudo yum install -y docker  
>sudo systemctl start docker  
>sudo systemctl enable docker  
>docker --version
If the docker --version command returned output, it confirmed successful installation.


CI/CD Pipeline – Concept Overview
We were introduced to the Continuous Integration and Continuous Deployment (CI/CD) Pipeline, which automates the building, testing, and deployment of applications. A basic pipeline was demonstrated using AWS services and Docker.

CI/CD Flow (Demonstrated):
>pgsql
>Copy
>Edit
START ➝ IAM User ➝ EC2 Linux Instance ➝ Dev Policy ➝ CI Config ➝ Docker ➝ Deploy Application ➝ END
We also discussed mini pipelines, where small changes (like adding a new feature) are deployed quickly and efficiently.

Docker Hands-On: HTML/NodeJS App Deployment
As part of the hands-on lab, we deployed a sample static website (Calculator App) using Docker.

Commands Used:
cd Calculator_using_htmlcssjs – Changed to the project directory

ls -la – Listed files with permissions

pwd – Printed working directory

nano Dockerfile – Opened and created the Dockerfile

🛠 Sample Dockerfile:
Dockerfile
Copy
Edit
FROM busybox:latest  
WORKDIR /www  
COPY . /www  
EXPOSE 80  
CMD ["httpd", "-f", "-v", "-p", "80"]

Build and Run Docker Container:
bash
Copy
Edit
docker build -t my-app .  
docker run -d -p 80:80 my-app

Configuring EC2 Security Group for Web Access:
Navigated to EC2 > Security Groups > launch-wizard-xx

Clicked Edit Inbound Rules

Added a new rule:

Type: Custom TCP

Port Range: 80

Source: Anywhere (IPv4)

Saved changes to enable web traffic access


Accessing the Web Application:
Opened a web browser

Entered the EC2 instance's Public IP in the address bar

The calculator web app hosted inside the Docker container was successfully displayed

Outcomes:
The third day’s session provided valuable hands-on exposure to cloud infrastructure and deployment automation. We learned to securely manage users via IAM, launch and connect to cloud servers using EC2, install and use Docker, and deploy a web application. These foundational skills are essential for setting up efficient DevOps workflows and future automation.

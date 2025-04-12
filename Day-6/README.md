Date: 03/04/2025

Day 6 – Kubernetes Deployment & Jenkins CI/CD Integration

On the final day of our DevOps Skill Lab training, we implemented automated deployment pipelines using Jenkins and configured Kubernetes deployments through YAML files. We also explored service exposure options in Kubernetes and set up Jenkins on an EC2 instance for CI/CD integration.

Kubernetes Deployment Configuration with YAML
We configured a Deployment and ReplicaSet using a YAML file to deploy a containerized IPL application in a specific namespace.

Deployment YAML: blue-deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: blue-deploy
  namespace: blue-ns
spec:
  replicas: 5
  selector:
    matchLabels:
      app: ipl
  template:
    metadata:
      labels:
        app: ipl
    spec:
      containers:
        - name: c-1
          image: daviddocker526/ipl-srh:latest
          ports:
            - containerPort: 80


Kubernetes Commands Used (EC2 Instance & Killercoda)
sudo su
kubectl create ns blue-ns
kubectl get ns
vi blue-deployment.yaml
kubectl apply -f blue-deployment.yaml
kubectl get deployment -n blue-ns
kubectl get rs -n blue-ns
kubectl get pods -n blue-ns
kubectl describe pod <pod-name> -n blue-ns


Service YAML: blue-service.yaml

apiVersion: v1
kind: Service
metadata:
  name: blue-service
  namespace: blue-ns
spec:
  selector:
    app: ipl
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer


Service Types:

1. ClusterIP – Default, accessible within cluster

2. NodePort – Exposes the service on each Node’s IP at a static port

3. LoadBalancer – Provides external IP (pending in Killercoda due to paid service)

4. ExternalName – Maps service to DNS name


cat blue-service.yaml
kubectl apply -f blue-service.yaml
kubectl get all -n blue-ns

Note: In Killercoda, LoadBalancer type shows Pending due to lack of cloud integration.

Managing Pods & Deployments

kubectl delete pod <pod-name> -n blue-ns
kubectl get pods -n blue-ns

To edit YAML file:

Press i to insert

Save: Esc + :wq

To scale down/up replicas:
vi blue-deployment.yaml  # modify replicas
kubectl apply -f blue-deployment.yaml

To delete resources:
kubectl delete deployment blue-deploy -n blue-ns
kubectl delete svc blue-service -n blue-ns


Jenkins for CI/CD Automation
Jenkins was introduced as a CI/CD tool to automate deployments (unlike Kubernetes manual deployment).

EC2 Jenkins Setup
Instance type: t3.medium

Storage: 20 GB

Security Group: Enable TCP on port 22 (SSH) and 8080 (Jenkins)

Connect using PuTTY (use key pair)

sudo su
apt update -y

Jenkins Installation on Ubuntu

sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins

Also install Java:
sudo apt update
sudo apt install openjdk-11-jdk
java --version

Jenkins Web Setup
Access via: http://<EC2-Public-IP>:8080

Unlock Jenkins using:
cat /var/lib/jenkins/secrets/initialAdminPassword

Install suggested plugins

Create first admin user

Save and continue to dashboard


Jenkins Plugins for Kubernetes
Install the following plugins from Manage Jenkins > Plugins > Available:

-AWS Credentials

-Kubernetes

-Kubernetes CLI

-Kubernetes :: Pipeline :: DevOps Steps

-Kubernetes Client API

-Kubernetes Credentials

-Kubernetes Credentials Provider


AWS Integration & kubeconfig in Jenkins
Generate AWS access keys in EC2

Add credentials in Jenkins:

Go to Manage Jenkins → Credentials → Global → Add Credentials

Select AWS credentials, paste Access Key ID & Secret, add ID & description

Install kubectl, unzip, and awscli in Jenkins server:

bash
Copy
Edit
sudo apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
Configure AWS CLI:

bash
Copy
Edit
aws configure
Switch to Jenkins user:

bash
Copy
Edit
sudo su - jenkins
Get EKS kubeconfig file (from commands shared in the Word document)

Use cat config to view and copy contents

Add kubeconfig as Jenkins credential


Jenkins Pipeline for Deployment
Go to Dashboard → New Item → Pipeline

Paste the EKS deployment pipeline script (from Word doc)

Set Git repository URL for pipeline

Save and build

Check logs under "Build Now" for execution details

Final Verification:
bash
Copy
Edit
kubectl get all -n blue-ns

-Verify app deployment and services are running correctly.



Final Outcome:

Over the course of the 6-day DevOps Skill Lab training, we gained practical, end-to-end exposure to modern DevOps practices by implementing a fully automated CI/CD pipeline using Docker, Kubernetes, and Jenkins. We started by containerizing an IPL web application with Docker, creating Docker images and pushing them to Docker Hub. This was followed by orchestrating containers on Kubernetes using EKS, where we configured deployments, replica sets, and services through YAML manifests. We also explored namespace management, pod scaling, and different service types including LoadBalancer.

The final phase focused on Jenkins integration, where we automated the deployment process by creating pipelines that pulled code from GitHub, built Docker images, and deployed them to EKS clusters. Jenkins was configured on an EC2 instance with necessary plugins and AWS credentials. Overall, the lab enabled us to understand and implement the complete DevOps lifecycle—from coding and building to deploying and monitoring—on a cloud-native infrastructure, setting a solid foundation for real-world DevOps workflows.


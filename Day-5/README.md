Date: 02/04/2025

Day 5 – Kubernetes Basics and Cluster Setup

On Day 5 of our DevOps Skill Lab training, we moved beyond Docker and learned about Kubernetes (also known as K8s), a powerful container orchestration tool. We explored the need for Kubernetes, its core features, architecture, and the step-by-step procedure to install tools like `kubectl`, `eksctl`, and `awscli`. We also practiced deploying applications using YAML configuration files.

Drawbacks of Docker:
We started the session by understanding the limitations of Docker that lead to the need for Kubernetes:
- Containers are not self-maintained.
- Docker lacks built-in load balancing.
- Docker does not support auto-scaling.

Introduction to Kubernetes:
Kubernetes is a container orchestration tool designed to manage containerized applications across a cluster of machines. It automates deployment, scaling, and operations of application containers.

History:
- Developed by Google.
- Donated to CNCF (Cloud Native Computing Foundation) in 2014.

Key Features of Kubernetes:
1. **Autoscaling** – Automatically increases/decreases resources based on traffic.
2. **Auto-healing** – Recreates deleted or failed resources.
3. **Load Balancing** – Distributes traffic evenly across servers.
4. **Platform Independence** – Works on any OS.
5. **Rollback** – Supports switching to previous stable versions.
6. **Health Monitoring** – Constantly monitors the health of containers.
7. **Fault Tolerance** – Alerts when nodes go down and ensures continuity.
8. **Orchestration** – Central management of all Kubernetes resources.

Kubernetes Architecture:
Kubernetes clusters consist of two types of nodes:

**1. Master Node:**
- **API Server:** Entry point for all Kubernetes commands.
- **etcd:** Key-value store for cluster data.
- **Controller Manager:** Handles cluster control processes.
- **Scheduler:** Assigns tasks to worker nodes.

**2. Worker Node:**
- **Kubelet:** Communicates with master, runs containers via pods.
- **Pod:** Smallest deployable unit in Kubernetes.
- **Container Engine:** Runs containers.
- **Kube-proxy:** Manages networking.

Steps to Create a Cluster using EC2:
1. Launch EC2 instance:
   - Ubuntu OS
   - Instance type: t2.medium
   - Allow SSH & HTTP
2. Connect to EC2 instance:
   ```bash
   sudo su
   apt update -y
   ```

Install `kubectl`:
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
kubectl version --client
```

Install `eksctl`:
```bash
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH
curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz
sudo mv /tmp/eksctl /usr/local/bin
```

Install `awscli`:
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version
```

Access Key Setup:
1. Create IAM user > Attach Administrator Access policy.
2. Generate access keys and download the `.csv`.
3. Configure AWS credentials:
```bash
aws configure
```

Create EKS Cluster:
```bash
eksctl create cluster \
--name blue-cluster \
--region sa-east-1 \
--zone sa-east-1a,sa-east-1b \
--nodegroup-name red-node \
--node-type t2.medium \
--nodes 2
```

Kubernetes Practice Using EC2:
```bash
kubectl get nodes
kubectl get namespace
kubectl create namespace white
kubectl get namespace
```

YAML File for Namespace:
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: white-2
```
Commands:
```bash
touch blue.yaml
vi blue.yaml
kubectl apply -f blue.yaml
```

YAML File for Pod:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: blue-pod2
  namespace: white-2
spec:
  containers:
    - name: c-1
      image: daviddocker526/ipl
      ports:
        - containerPort: 80
```
Commands:
```bash
kubectl apply -f blue-pod.yaml
kubectl get pods -n white-2
kubectl logs blue-pod2 -n white-2
kubectl describe pod blue-pod2 -n white-2
kubectl delete pod blue-pod2 -n white-2
```

ReplicaSet Concept:
Ensures desired number of pod replicas are always running. Handles pod failures automatically.

YAML File for ReplicaSet:
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: blue-replica1
  namespace: white-2
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
        -  name: c-2
           image: daviddocker526/ipl
           ports:
             - containerPort: 80
```
Commands:
```bash
kubectl apply -f white-replica.yaml
kubectl get rs -n white-2
kubectl get pods -n white-2
```

Outcomes:
We explored why Kubernetes is needed over Docker, learned about its architecture, and practiced deploying resources using YAML files. We created a namespace, deployed pods, and managed replicas through ReplicaSets, helping us grasp container orchestration in a real-world environment.





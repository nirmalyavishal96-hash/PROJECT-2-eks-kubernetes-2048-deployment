# 🚀 Deploying 2048 Game on Kubernetes (Minikube → AWS EKS)

This project demonstrates deploying a containerized application on Kubernetes locally using Minikube and then deploying the same application on AWS EKS.

The application deployed is the **2048 game**, exposed publicly using an AWS Load Balancer.

---

# 📌 Project Architecture

## Local Development (Minikube)

Developer Laptop  
↓  
Minikube Kubernetes Cluster  
↓  
Deployment  
↓  
Pods  
↓  
Service  

---

## Cloud Deployment (AWS EKS)

Internet  
↓  
AWS Elastic Load Balancer  
↓  
Kubernetes Service (LoadBalancer)  
↓  
Pods (2048 Application)  
↓  
ReplicaSet  
↓  
Deployment  
↓  
EKS Worker Node (EC2)  
↓  
Amazon EKS Control Plane  

---

# 🛠 Tools & Technologies Used

- Kubernetes
- Minikube
- AWS EKS
- Docker
- kubectl
- eksctl
- AWS CLI
- GitHub

---

# 📂 Project Structure

```
PROJECT-2-eks-kubernetes-2048-deployment
│── architecture
|   ├── architecture-README.md
|   ├── eks-2048-architecture.png
├── kubernetes
│   ├── deployment.yaml
│   └── service.yaml
│
├── screenshots
|   ├── 2048-game.png
│   ├── eks-nodes.png 
|   ├── loadbalancer-service.png
|   ├── pods-running.png
└── README.md
```

---

# ⚙️ Step 1 – Run Kubernetes Locally (Minikube)

Start Minikube

```bash
minikube start
```

Check cluster

```bash
kubectl get nodes
```

Deploy application

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

Check pods

```bash
kubectl get pods
```

Expose service

```bash
kubectl port-forward service/sample-app-service 8080:80
```

Access application

```
http://localhost:8080
```

---

# ☁️ Step 2 – Deploy to AWS EKS

### Install eksctl

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/local/bin
```

Verify installation

```bash
eksctl version
```

---

# Create EKS Cluster

```bash
eksctl create cluster \
--name sample-eks-cluster \
--region ap-south-1 \
--node-type t3.small \
--nodes 1
```

Check nodes

```bash
kubectl get nodes
```

---

# Deploy Kubernetes Resources

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

Check pods

```bash
kubectl get pods
```

---

# Expose Application

```bash
kubectl expose deployment sample-app \
--type=LoadBalancer \
--name=sample-app-lb \
--port=80 \
--target-port=80
```

Check service

```bash
kubectl get svc
```

Access application via LoadBalancer URL.

---

# 🔄 Rolling Update Example

Update container image

```bash
kubectl set image deployment/sample-app sample-app=public.ecr.aws/l6m2t8p7/docker-2048:latest
```

Check rollout

```bash
kubectl rollout status deployment sample-app
```

Rollback deployment

```bash
kubectl rollout undo deployment sample-app
```

---

# 🔧 Challenges & Debugging

## Issue 1 – ImagePullBackOff

Error:

```
ImagePullBackOff
```

Cause:

The container image used an outdated Docker manifest format.

Fix:

Updated image to

```
public.ecr.aws/l6m2t8p7/docker-2048:latest
```

---

## Issue 2 – Too Many Pods Error

Error:

```
0/1 nodes are available: Too many pods
```

Cause:

Single EKS worker node has limited IP addresses.

Fix:

Wait for rolling update to complete or scale replicas.

---

## Issue 3 – DNS Issue in Minikube

Error:

```
sample.local not resolving
```

Cause:

WSL networking conflict with Windows host file.

Fix:

Used port-forwarding.

```
kubectl port-forward service/sample-app-service 8080:80
```

---

# 📸 Screenshots

Add screenshots of:

- Running Pods
- LoadBalancer Service
- EKS Node
- 2048 Game UI

---

# 🧹 Cleanup

To avoid AWS charges delete the cluster.

```bash
eksctl delete cluster --name vishal-eks-cluster --region ap-south-1
```

---

# 📚 Learning Outcomes

- Kubernetes deployment management
- Rolling updates and rollback
- Kubernetes services and networking
- Deploying applications on AWS EKS
- Debugging Kubernetes deployment issues

---

# 👨‍💻 Author

Nirmalya Das   
DevOps Enthusiatic
📐 Architecture Overview



This project demonstrates deploying a containerized application on Kubernetes using both local and cloud environments.

The application used in this project is the 2048 game, deployed using Kubernetes Deployment, scaled using ReplicaSets, and exposed externally through an AWS Elastic Load Balancer when running on Amazon EKS.

The project follows a DevOps workflow:

Local Development → Kubernetes Validation → Cloud Deployment → Public Access

The application is first deployed and tested locally using Minikube, and then the same Kubernetes manifests are deployed to Amazon EKS for production-style deployment.

🏗 System Architecture

This project demonstrates two deployment environments:

1️⃣ Local Kubernetes Cluster (Minikube)

Used for:

Development

Testing Kubernetes manifests

Debugging before cloud deployment

Flow:

Developer Laptop
        │
        ▼
   Minikube Cluster
        │
        ▼
     Deployment
        │
        ▼
     ReplicaSet
        │
        ▼
   5 Pods (2048 App)
        │
        ▼
   ClusterIP Service
        │
        ▼
kubectl port-forward



2️⃣ Production Deployment (AWS EKS)

The same application is deployed on Amazon EKS for a production-style environment.

Flow:

Internet
   │
   ▼
AWS Elastic Load Balancer
   │
   ▼
Kubernetes Service (LoadBalancer)
   │
   ▼
ReplicaSet
   │
   ▼
5 Pods (2048 Container)
   │
   ▼
Deployment
   │
   ▼
EC2 Worker Node
   │
   ▼
Amazon EKS Control Plane



⚙️ Key Architecture Components
Component	Purpose
Deployment	Manages application lifecycle and updates
ReplicaSet	Ensures desired number of pods are running
Pods (5 replicas)	Run the containerized 2048 application
Service (ClusterIP)	Internal communication within cluster
Service (LoadBalancer)	Exposes application to the internet
Amazon EKS	Managed Kubernetes service
EC2 Worker Nodes	Run Kubernetes workloads


🔁 High Availability

The deployment uses 5 pod replicas, providing:

Load distribution

Fault tolerance

Self-healing

High availability

If any pod fails, Kubernetes automatically recreates it.

🚀 DevOps Workflow Demonstrated

This architecture demonstrates a real-world DevOps deployment flow:


Application Containerization
        ↓
Local Kubernetes Testing (Minikube)
        ↓
Cloud Deployment (Amazon EKS)
        ↓
Public Exposure via Load Balancer
        ↓
Scalable & Highly Available Application


🧰 Tech Stack

Category	                   Tools Used
Containerization	              Docker
Container Orchestration	        Kubernetes
Local Kubernetes	             Minikube
Cloud Provider	                   AWS
Managed Kubernetes	            Amazon EKS
Infrastructure CLI	              eksctl
Kubernetes CLI	                  kubectl
Version Control	                Git & GitHub


📌 What This Architecture Demonstrates

This project highlights practical experience with:

Kubernetes Deployments

ReplicaSets and Pod scaling

Kubernetes Services

LoadBalancer networking

Cloud-native application deployment

Deploying workloads on Amazon EKS
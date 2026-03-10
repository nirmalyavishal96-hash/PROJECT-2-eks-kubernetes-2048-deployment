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

---



⚙️ Key Architecture Components

    Component	                    Purpose

1. Deployment	  ------->          Manages application lifecycle and updates
2. ReplicaSet	      ------->      Ensures desired number of pods are running
3. Pods (5 replicas)	------->    Run the containerized 2048 application
4. Service (ClusterIP)	------->    Internal communication within cluster
5. Service (LoadBalancer) ------->	Exposes application to the internet
6. Amazon EKS	         ------->   Managed Kubernetes service
7. EC2 Worker Nodes	      ------->  Run Kubernetes workloads


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

---


🧰 Tech Stack

Category	                             Tools Used

1. Containerization	     ------->         Docker
2. Container Orchestration	 ------->     Kubernetes
3. Local Kubernetes	          ------->    Minikube
4. Cloud Provider	          ------->    AWS
5. Managed Kubernetes	    ------->      Amazon EKS
6. Infrastructure CLI	     ------->     eksctl
7. Kubernetes CLI	         ------->     kubectl
8. Version Control	         ------->     Git & GitHub


📌 What This Architecture Demonstrates

This project highlights practical experience with:

1. Kubernetes Deployments

2. ReplicaSets and Pod scaling

3. Kubernetes Services

4. LoadBalancer networking

5. Cloud-native application deployment

6. Deploying workloads on Amazon EKS
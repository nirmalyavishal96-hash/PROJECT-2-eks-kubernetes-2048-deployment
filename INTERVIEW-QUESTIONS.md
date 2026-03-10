Kubernetes & AWS EKS Interview Questions

This document contains commonly asked interview questions and answers related to the concepts implemented in this project.

The questions focus on:

Kubernetes architecture

Deployments

Pods

Services

Scaling

Debugging

AWS EKS

These questions can help revise the core DevOps concepts demonstrated in this project.

1. What is Kubernetes?

Kubernetes is an open-source container orchestration platform used to automate the deployment, scaling, and management of containerized applications.

It helps manage containers across a cluster of machines.

Key features include:

Automated deployment

Auto scaling

Load balancing

Self-healing

Rolling updates

2. What is a Pod in Kubernetes?

A Pod is the smallest deployable unit in Kubernetes.

A pod contains one or more containers that share:

Network

Storage

Lifecycle

In this project, each pod runs the 2048 containerized application.

3. What is a Deployment?

A Deployment is a Kubernetes resource that manages the lifecycle of applications.

It allows you to:

Deploy applications

Update container images

Scale pods

Perform rolling updates

Rollback changes

Example command used in this project:

kubectl apply -f deployment.yaml

4. What is a ReplicaSet?

A ReplicaSet ensures that a specified number of pod replicas are running at all times.

If a pod crashes or is deleted, the ReplicaSet automatically creates a new one.

Example from this project:

replicas: 5

This ensures five pods are always running.

5. What is the difference between Deployment and ReplicaSet?

Deployment	ReplicaSet
Manages application updates	Ensures desired number of pods
Supports rolling updates	Does not manage updates
Higher-level abstraction	Lower-level controller

A Deployment automatically creates and manages ReplicaSets.

6. What is a Kubernetes Service?

A Service is used to expose Kubernetes pods so that they can communicate with other services or external users.

Types of services include:

ClusterIP

NodePort

LoadBalancer

ExternalName

In this project, the application was exposed using a LoadBalancer service.

7. What is ClusterIP?

ClusterIP is the default service type in Kubernetes.

It exposes the service only inside the Kubernetes cluster.

Other pods inside the cluster can communicate with it using the ClusterIP.

8. What is a LoadBalancer Service?

A LoadBalancer service exposes an application externally.

When deployed on AWS EKS, Kubernetes automatically provisions an:

AWS Elastic Load Balancer

This provides a public endpoint for the application.

9. What is Amazon EKS?

Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service provided by AWS.

AWS manages:

Kubernetes control plane

High availability

Cluster management

Users manage:

Worker nodes

Applications

Kubernetes resources

10. What is Minikube?

Minikube is a tool that allows developers to run a local Kubernetes cluster on their machine.

It is commonly used for:

Learning Kubernetes

Testing deployments

Development environments

11. What is Rolling Update?

A rolling update gradually replaces old pods with new ones.

This ensures the application remains available during updates.

Example command:

kubectl set image deployment/sample-app sample-app=new-image

12. What is Rollback in Kubernetes?

Rollback allows you to revert a deployment to a previous version.

Command used:

kubectl rollout undo deployment sample-app

This restores the previous ReplicaSet.

13. What is Self-Healing in Kubernetes?

Self-healing means Kubernetes automatically replaces failed pods.

Example:

If a pod crashes or is deleted:

kubectl delete pod <pod-name>

The ReplicaSet automatically creates a new pod.

14. What is kubectl?

kubectl is the command-line tool used to interact with Kubernetes clusters.

Common commands used in this project:

kubectl get pods
kubectl get svc
kubectl apply -f deployment.yaml
kubectl describe pod <pod-name>

15. What is eksctl?

eksctl is a CLI tool used to create and manage Amazon EKS clusters.

Example command used in this project:

eksctl create cluster \
--name vishal-eks-cluster \
--region ap-south-1 \
--node-type t3.small \
--nodes 1

16. What debugging issues did you face in this project?

Issue 1 – ImagePullBackOff

Error:

ImagePullBackOff

Cause:

The container image used an outdated Docker manifest format.

Fix:

Updated the container image to a compatible version.

Issue 2 – Too Many Pods Error

Error:

0/1 nodes are available: Too many pods

Cause:

A single EC2 worker node had limited IP capacity.

Fix:

Waited for the rolling update to complete or scaled replicas appropriately.

Issue 3 – DNS issue with Minikube

Error:

sample.local not resolving

Cause:

WSL networking conflict with Windows host configuration.

Fix:

Used port forwarding.

kubectl port-forward service/sample-app-service 8080:80

17. How does Kubernetes ensure high availability?

Kubernetes ensures high availability by:

Running multiple pod replicas

Automatically recreating failed pods

Using load balancing

Performing rolling updates

In this project:

5 pod replicas were deployed

to maintain application availability.

18. What happens when you delete a pod?

If a pod managed by a ReplicaSet or Deployment is deleted:

Kubernetes automatically recreates a new pod.

Example:

kubectl delete pod sample-app-xxxx

A new pod will be created automatically.

19. What is the role of a Kubernetes Deployment in this project?

In this project, the Deployment was responsible for:

Managing the lifecycle of the 2048 application

Ensuring the desired number of pods were running

Performing rolling updates when the container image was updated

20. How was the application exposed publicly in this project?

The application was exposed using a LoadBalancer service.

This created an AWS Elastic Load Balancer automatically, which allowed users to access the application via a public URL.
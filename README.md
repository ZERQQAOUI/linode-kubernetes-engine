Project Overview: Deploying MongoDB and Mongo-Express on Kubernetes
Table of Contents
Overview
Prerequisites
Deployment Steps
1. Create Kubernetes Cluster on LKE
2. Set Up Kubeconfig
3. Deploy MongoDB with Helm
4. Deploy Mongo-Express
5. Deploy Ingress Controller
Ingress Rules
Overview
This project involves building and deploying a MongoDB cluster on a Linode Kubernetes Engine (LKE) cluster. The deployment includes the use of Helm charts for managing MongoDB and Nginx-Ingress, ensuring seamless access to the database through the Mongo-Express UI client.

Prerequisites
Before starting, make sure you have the following in place:

Linode Kubernetes Engine cluster created.
Helm installed on your local machine (Helm Installation Guide).
Linode Block Storage for data persistence.
Deployment Steps
1. Create Kubernetes Cluster on LKE
Use Linode's Kubernetes Engine to create a cluster. The master nodes are managed for you.

2. Set Up Kubeconfig
Export your Kubeconfig file (credentials) and set it as an environmental variable:


export KUBECONFIG=test-kubeconfig.yaml
3. Deploy MongoDB with Helm
Add Bitnami Helm repository:


helm repo add bitnami https://charts.bitnami.com/bitnami
Search for MongoDB Helm chart:


helm search repo bitnami/mongodb
Create a values file (mongodb-values.yaml) to define MongoDB configuration:


helm install my-mongodb --values mongodb-values.yaml bitnami/mongodb
4. Deploy Mongo-Express
Create a configuration file (mongo-express-deployment.yaml) for Mongo-Express deployment and service.

Ensure environmental variables for connecting Mongo-Express to MongoDB are set.

Apply the configuration:

kubectl apply -f mongo-express-deployment.yaml
5. Deploy Ingress Controller
Use Helm charts to deploy the Nginx-Ingress controller:


helm install nginx-ingress stable/nginx-ingress --set ...
Note: A Linode NodeBalancer is automatically created, serving as the entry point to the cluster.

Ingress Rules
Create Ingress rules to handle incoming requests:

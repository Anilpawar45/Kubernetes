# Ingress Deployment
This repository contains the configuration files for deploying an Ingress in a Kubernetes cluster. Ingress is used to manage external access to services within the cluster, providing HTTP and HTTPS routing.
## Why Use Ingress?
Without Ingress, you typically expose services using:

NodePort – Assigns a port on each node.
LoadBalancer – Provisions a cloud provider's load balancer.
ClusterIP – Only accessible within the cluster.
Ingress provides a more scalable and efficient way to manage external access with features like:

Path-based routing (e.g., /app1 → service1, /app2 → service2)
Host-based routing (e.g., app.example.com → service1, api.example.com → service2)
TLS termination (HTTPS)
Rewrite and redirect rules
Authentication and security mechanisms


![image](https://github.com/user-attachments/assets/470122fa-b401-48f9-9e42-581b4d0bf547)


**Deployment.yaml**

'''bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: home-page
spec:
  selector:
    matchLabels:
      app: home-page
  template:
    metadata:
      labels:
        app: home-page
    spec:
      containers:
      - name: home-page
        image: httpd:alpine
        ports:
        - containerPort: 80
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mobile-page
spec:
  selector:
    matchLabels:
      app: mobile-page
  template:
    metadata:
      labels:
        app: mobile-page
    spec:
      containers:
      - name: mobile-page
        image: nginx
        ports:
        - containerPort: 80
        '''**
   1. ** command **
     ''' bash
       kubectl get pods
      '''     

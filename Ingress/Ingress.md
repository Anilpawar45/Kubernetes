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


### Deployment.yaml
```
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

```
### Service.yaml
```
apiVersion: v1
kind: Service
metadata:
  name: home-page-service
  labels:
    app: home-page-service
    env: devops
spec:
  selector:
    app: home-page
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 80
---

apiVersion: v1
kind: Service
metadata:
  name: mobile-page-serivce
  labels:
    app: mobile-page-serivce
    env: devops
spec:
  selector:
    app: mobile-page
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 80
   ```
### Ingress.yaml
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-anil
  labels:
    name: ingress-anil
spec:
  rules:
  - host: anil.com
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: home-page-service
            port: 
              number: 80
  - host: anil.mobile.com
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: mobile-page-serivce
            port: 
              number: 80




```
### Then push all files in git hub repository
```
git add .
git commit -m "create ingress file"
git push https://github.com/Anilpawar45/Kubernetes.git main
```
### clone repositories
```
git clone https://github.com/Anilpawar45/Kubernetes.git main
cd Kubernetes/
ls
```
### create pods,nods and container
show file 
1.deployment.yaml
2.service.yaml
3.Ingress.yaml
```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f Ingress.yaml
```
```
kubectl get pods
kubectl get deploy
kubectl get service
kubectl get namespace
```
minikube addons enable ingress
kubectl get pods -n ingress-nginx


```
kubectl get pods -o wide
minikube ssh
curl 10.244.0.6

![Screenshot (22)](https://github.com/user-attachments/assets/075e11e1-32d1-4b4f-8513-66742468bf82)
![Screenshot (24)](https://github.com/user-attachments/assets/b33e0c76-30c8-490f-a967-ad4b346de8b1)






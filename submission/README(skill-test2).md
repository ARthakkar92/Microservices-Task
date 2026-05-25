# Microservices Application Deployment on Kubernetes (AWS EKS)

## Objective

Deploy a microservices-based Node.js application on Kubernetes using AWS EKS, ensuring proper service communication, health checks, and API accessibility.

---

# Project Architecture

This project contains four Node.js microservices:

| Service         | Port | Description                                      |
| --------------- | ---- | ------------------------------------------------ |
| User Service    | 3000 | Handles user data                                |
| Product Service | 3001 | Handles product data                             |
| Order Service   | 3002 | Handles order data                               |
| Gateway Service | 3003 | API Gateway routing requests to backend services |

---

# Repository Structure

```text
submission/
├── deployments/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
├── services/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
├── screenshots/
│   ├── pods.png
│   ├── logs.png
│   └── service-test.png
└── README.md
```

---

# Technologies Used

* Docker
* Kubernetes
* AWS EKS
* kubectl
* Docker Hub
* Node.js

---

# Docker Image Creation

Docker images were built and pushed to Docker Hub.

## Example Build Command

```bash
Docker build -t ankitthakkar/user-service:latest \
-f submission/user-service/Dockerfile \
Microservices/user-service
```

## Push Images to Docker Hub

```bash
Docker push ankitthakkar/user-service:latest
Docker push ankitthakkar/product-service:latest
Docker push ankitthakkar/order-service:latest
Docker push ankitthakkar/gateway-service:latest
```

---

# Kubernetes Cluster Setup

AWS EKS cluster was used instead of Minikube as approved.

## Configure kubectl for EKS

```bash
aws eks update-kubeconfig \
--region ap-south-1 \
--name Ankit_EKS_cluster
```

## Verify Cluster Connectivity

```bash
kubectl get nodes
```

---

# Deployment Process

## Apply Kubernetes Deployments

```bash
kubectl apply -f deployments/
```

## Apply Kubernetes Services

```bash
kubectl apply -f services/
```

## Verify Pods

```bash
kubectl get pods -o wide
```

## Verify Services

```bash
kubectl get svc
```

---

# Kubernetes Features Implemented

## Deployments

Each deployment includes:

* Container image references
* Labels and selectors
* Resource requests and limits
* Environment variables
* Liveness probes
* Readiness probes

## Services

ClusterIP services were configured for:

* Internal communication
* Kubernetes DNS-based service discovery
* Inter-service routing

---

# Health Check Configuration

All services expose a `/health` endpoint.

Example:

```yaml
readinessProbe:
  httpGet:
    path: /health
    port: 3000

livenessProbe:
  httpGet:
    path: /health
    port: 3000
```

---

# Service Testing

Testing was performed using `kubectl port-forward`.

## Port Forward Gateway Service

```bash
kubectl port-forward svc/gateway-service 3003:3003
```

---

# API Testing Commands

## Health Endpoint

```bash
curl http://localhost:3003/health
```

Expected Output:

```json
{"status":"Gateway Service is healthy"}
```

---

## User Service API

```bash
curl http://localhost:3003/api/users
```

Expected Output:

```json
[{"id":1,"name":"John Doe"},{"id":2,"name":"Jane Smith"}]
```

---

## Product Service API

```bash
curl http://localhost:3003/api/products
```

Expected Output:

```json
[{"id":1,"name":"Laptop","price":999},{"id":2,"name":"Phone","price":699}]
```

---

## Order Service API

```bash
curl http://localhost:3003/api/orders
```

Expected Output:

```json
[]
```

---

# Inter-Service Communication Validation

The Gateway Service communicates internally with:

* user-service
* product-service
* order-service

using Kubernetes DNS service discovery.

Example internal communication:

```text
http://user-service:3000/users
http://product-service:3001/products
http://order-service:3002/orders
```

---

# Troubleshooting

## Check Pod Logs

```bash
kubectl logs <pod-name>
```

## Describe Pod

```bash
kubectl describe pod <pod-name>
```

## Common Issue Fixed

### Problem

Liveness and readiness probes were failing with HTTP 404.

### Root Cause

Probe path was incorrectly configured as `/`.

### Resolution

Updated probe path to `/health`.

---



# Screenshots

| ----------------    | ------------------------------------------------ |
| File Name           | Description                                      |
| ----------------    | ------------------------------------------------ |
| pods.png            | Output of `kubectl get pods`                     |
| logs.png            | service communication validation                 |
| URL_Testing.png     | Browser/API testing using localhost port-forward |
| Port-forwording.png | screenshot of port-forwording
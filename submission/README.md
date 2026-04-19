## Microservices Docker Assignment
---
## Overview

This project demonstrates containerization and orchestration of Node.js microservices using Docker and Docker Compose.

Services Included
User Service → Port 3000
Product Service → Port 3001
Order Service → Port 3002
Gateway Service → Port 3003

## Project Structure
submission/
├── user-service/
│   └── Dockerfile
├── product-service/
│   └── Dockerfile
├── order-service/
│   └── Dockerfile
├── gateway-service/
│   └── Dockerfile
├── compose.yaml
└── README.md

## Steps to Run
Navigate to submission folder:
cd submission
Build and start all services:
docker-compose up --build
Verify containers are running:
docker ps

## Service Endpoints
Service	URL
User Service	http://localhost:3000
Product Service	http://localhost:3001
Order Service	http://localhost:3002
Gateway Service	http://localhost:3003

## Screenshot

<img width="850" height="248" alt="image" src="https://github.com/user-attachments/assets/ce09aefd-5599-4d7c-bfd4-89a220b3ce07" />

<img width="766" height="191" alt="image" src="https://github.com/user-attachments/assets/ed3a19ca-e5d0-4b7a-b35f-c33493b3c0e5" />

<img width="703" height="240" alt="image" src="https://github.com/user-attachments/assets/3b6040b5-077e-4ac5-bd99-f1f624151279" />

<img width="766" height="256" alt="image" src="https://github.com/user-attachments/assets/8a772d7b-9c3c-46e9-82b8-0ed5e6971096" />

<img width="894" height="344" alt="image" src="https://github.com/user-attachments/assets/00904711-ec4e-4e4c-b5a3-04b01d0c0301" />

<img width="789" height="258" alt="image" src="https://github.com/user-attachments/assets/10b24091-a09e-4082-b11e-e234c05c596f" />






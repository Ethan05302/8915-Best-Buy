# Best Buy Cloud-Native Application

## 🛠 Application Architecture

This project is a cloud-native microservices-based application for Best Buy's online store. It follows the architecture of the Algonquin Pet Store (On Steroids), with the key difference that **Azure Service Bus** is used as a managed order queue instead of RabbitMQ.

![Architecture Diagram](./Deployment%20Files/architecture.png)

## 🧩 Microservices Overview

| Service         | Description                                                |
|-----------------|------------------------------------------------------------|
| Store-Front     | Frontend app for customers to browse and place orders.     |
| Store-Admin     | Admin interface for staff to manage products/orders.       |
| Product-Service | Handles CRUD operations on product data (MongoDB).         |
| Order-Service   | Receives orders and sends them to Azure Service Bus.       |
| Makeline-Service| Listens to order queue and inserts into MongoDB.           |
| AI-Service      | Uses GPT-4 and DALL·E to generate product info and images. |
| MongoDB         | Stores product and order data.                             |

## 🚀 Deployment Instructions

1. Ensure your Kubernetes cluster is running (e.g., Minikube, AKS).
2. Apply MongoDB StatefulSet:
   ```bash
   kubectl apply -f Deployment Files/mongodb-statefulset.yaml
   ```
3. Create Azure Service Bus secrets:
   ```bash
   kubectl apply -f Deployment Files/azure-sb-secret.yaml
   ```
4. Deploy all microservices:
   ```bash
   kubectl apply -f Deployment Files/order-service-deployment.yaml
   kubectl apply -f Deployment Files/makeline-service-deployment.yaml
   kubectl apply -f Deployment Files/product-service-deployment.yaml
   kubectl apply -f Deployment Files/store-front-deployment.yaml
   kubectl apply -f Deployment Files/store-admin-deployment.yaml
   kubectl apply -f Deployment Files/ai-service-deployment.yaml
   ```

## 📦 Microservice Repositories

| Service         | Repository Link |
|-----------------|------------------|
| Store-Front     | https://github.com/Ethan05302/bestbuy-store-front |
| Store-Admin     | https://github.com/Ethan05302/bestbuy-store-admin |
| Product-Service | https://github.com/Ethan05302/bestbuy-product-service |
| Order-Service   | https://github.com/Ethan05302/bestbuy-order-service |
| Makeline-Service| https://github.com/Ethan05302/bestbuy-makeline-service |
| AI-Service      | https://github.com/Ethan05302/bestbuy-ai-service |

## 🐳 Docker Images

| Service         | Docker Image Link |
|-----------------|-------------------|
| Store-Front     | https://hub.docker.com/r/ethan200530/store-front |
| Store-Admin     | https://hub.docker.com/r/ethan200530/store-admin |
| Product-Service | https://hub.docker.com/r/ethan200530/product-service |
| Order-Service   | https://hub.docker.com/r/ethan200530/order-service |
| Makeline-Service| https://hub.docker.com/r/ethan200530/makeline-service |
| AI-Service      | https://hub.docker.com/r/ethan200530/ai-service |

## 🎬 Demo Video

[Watch the 5-minute demo on YouTube](https://youtube.com/your-demo-video-link)

## ⚠️ Known Issues / Limitations

- None at this time. The application works end-to-end from order placement to queue processing.
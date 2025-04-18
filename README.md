Video Demo: https://youtu.be/R2aKFK1w3p8
# Best Buy Cloud-Native Application

## Application Architecture

This project is a cloud-native microservices-based application for Best Buy's online store. It follows the architecture of the Algonquin Pet Store (On Steroids), with the key difference that **Azure Service Bus** is used as a managed order queue instead of RabbitMQ.

![Digram](https://github.com/user-attachments/assets/9068749d-8d00-4c53-9595-612c67f79bd5)


## Microservices Overview

| Service         | Description                                                |
|-----------------|------------------------------------------------------------|
| Store-Front     | Frontend app for customers to browse and place orders.     |
| Store-Admin     | Admin interface for staff to manage products/orders.       |
| Product-Service | Handles CRUD operations on product data (MongoDB).         |
| Order-Service   | Receives orders and sends them to Azure Service Bus.       |
| Makeline-Service| Listens to order queue and inserts into MongoDB.           |
| AI-Service      | Uses GPT-4 and DALL·E to generate product info and images. |
| MongoDB         | Stores product and order data.                             |

## Deployment Instructions

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

## Microservice Repositories

| Service         | Repository Link |
|-----------------|------------------|
| Store-Front     |https://github.com/Ethan05302/89157|
| Store-Admin     | https://github.com/Ethan05302/89156|
| Product-Service | https://github.com/Ethan05302/89155|
| Order-Service   | https://github.com/Ethan05302/89154 |
| Makeline-Service| https://github.com/Ethan05302/89152 |
| AI-Service      | https://github.com/Ethan05302/8915 |

## Docker Images

| Service         | Docker Image Link |
|-----------------|-------------------|
| Store-Front     | https://hub.docker.com/r/ethan200530/store-front |
| Store-Admin     | https://hub.docker.com/r/ethan200530/store-admin |
| Product-Service | https://hub.docker.com/r/ethan200530/product-service |
| Order-Service   | https://hub.docker.com/r/ethan200530/order-service |
| Makeline-Service| https://hub.docker.com/r/ethan200530/makeline-service |
| AI-Service      | https://hub.docker.com/r/ethan200530/ai-service |

## Known Issues 

My ai-service pod is running fine and there are no errors in the logs. The text generation works, but the image generation isn't responding — it doesn't return any image.

I checked the code and the setup, and it looks okay, so I think the issue might be with the OpenAI API or network access. I’ll keep looking into it.

# Voguenest Full-Stack Kubernetes Project

![Architecture Diagram](/doc/diagram-export-28-01-2026-13_18_11.png) 

---

# 🛍️ VogueNest - Full Stack Docker Deployment

A production-inspired full-stack e-commerce application showcasing modern containerized deployment using **Docker**, **Nginx**, **Cloudflare Tunnel**, and **Jenkins CI/CD**.

---

## 🚀 Live Demo

🌐 **Application:** https://voguenest.tayolabs.dev

---

## 📖 Overview

VogueNest is a full-stack e-commerce platform built with modern web technologies and deployed using a production-inspired architecture.

The project demonstrates how to build, containerize, and deploy a scalable full-stack application where:

- The **React frontend** is served by Nginx.
- The **Node.js API** is load-balanced across three replicas using Nginx.
- The **MongoDB database** is containerized and only accessible within the Docker network.
- **Stripe test payment integration**
- The application is securely exposed to the internet through **Cloudflare Tunnel**.
- Deployment is automated using a **Jenkins CI/CD pipeline**.

The backend API is **not publicly accessible**. All API communication happens internally within the Docker network through a reverse proxy.

---

## 🏗️ Architecture

```text
                           Internet
                               │
                               ▼
                     Cloudflare Tunnel
                               │
                               ▼
                    Central Nginx Reverse Proxy
                     │                      │
                     ▼                      ▼
          React Frontend              API Load Balancer
            (Nginx)                        (Nginx)
                                             │
                   ┌─────────────┬─────────────┬─────────────┐
                   ▼             ▼             ▼
              API Replica 1  API Replica 2  API Replica 3
                       │
                       ▼
                    MongoDB
```

---

# ⚙️ Technology Stack

## Frontend

- React
- TypeScript
- Vite
- Axios
- Context API
- Custom Hooks

## Backend

- Node.js
- Express.js
- TypeScript
- MongoDB
- JWT Authentication
- Stripe Checkout

## Infrastructure

- Docker
- Docker Compose
- Nginx
- Cloudflare Tunnel
- Jenkins

---

# ✨ Features

### Frontend

- User Registration & Login
- Product Catalogue
- Shopping Cart
- Checkout
- Protected Routes
- Responsive Design
- Third-party Product API Integration
- Context API State Management
- Custom Hooks

### Backend

- JWT Authentication
- Refresh Token Support
- Stripe Checkout Integration
- Order Management
- Protected Routes
- Health Check Endpoint

---

# 📦 API Endpoints

| Method | Endpoint | Description | Auth |
|---------|----------|-------------|------|
| POST | `/signup` | Register a user | ❌ |
| POST | `/login` | Authenticate user | ❌ |
| POST | `/sign-out` | Logout user | ❌ |
| GET | `/users` | Retrieve users | ❌ |
| GET | `/health` | Health check | ❌ |
| POST | `/send-orders` | Create an order | ✅ |
| GET | `/orders` | Retrieve authenticated user's orders | ✅ |
| GET | `/refreshToken` | Refresh access token | ❌ |
| POST | `/create-checkout-session` | Create Stripe checkout session | ✅ |

---

# 📂 Project Structure

```text
.
├── VogueNest-Frontend/
├── VogueNest-API/
├── docker-compose.yml
├── Jenkinsfile
└── README.md
```

### Backend Structure

The API follows a clean layered architecture:

- Controllers
- Services
- Middleware
- Routers
- Schema
### Frontend Structure

The frontend is organised into:

- Pages
- Components
- Services
- Context
- Custom Hooks
- Utilities

---

# 🐳 Deployment Highlights

- Multi-container Docker Compose deployment
- React served with Nginx
- Three replicated API containers
- Nginx load balancing
- Private backend API
- Internal Docker networking
- Containerized MongoDB
- Secure public access via Cloudflare Tunnel
- Automated deployment using Jenkins

---

# 🔒 Security

- Backend API is **not publicly exposed**
- MongoDB is only accessible inside the Docker network
- Authentication using JWT
- Secure reverse proxy with Nginx
- Public traffic routed through Cloudflare Tunnel

---


# 🎯 Learning Objectives

This project demonstrates practical experience with:

- React + TypeScript
- Node.js + Express
- MongoDB
- Docker
- Docker Compose
- Nginx Reverse Proxy
- Nginx Load Balancing
- Cloudflare Tunnel
- Jenkins CI/CD
- Container Networking
- Production-inspired Deployment


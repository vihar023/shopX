# 🛒 shopX

![Java](https://img.shields.io/badge/Java-17%2B-orange)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen)
![Microservices](https://img.shields.io/badge/Architecture-Microservices-blue)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-blue)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![Kafka](https://img.shields.io/badge/Apache%20Kafka-Event%20Driven-black)

## 📌 Overview

**ShopX** is a cloud-native eCommerce platform built using **Java Spring Boot Microservices Architecture**.

The platform follows an enterprise-level microservices design by separating core business domains into independent, scalable, and independently deployable services, including **user management, product catalog, inventory management, order processing, payment processing, and notification services**.

Built with **Spring Boot, Spring Cloud, PostgreSQL, Apache Kafka, Docker, and DevOps practices**, ShopX demonstrates modern backend engineering concepts such as **API Gateway, Service Discovery, REST-based communication, event-driven architecture, JWT security, database-per-service design, and production-ready deployment patterns**.

The project focuses on building a scalable, maintainable, and resilient eCommerce system following industry-standard cloud-native architecture principles.

The platform provides complete eCommerce functionality, including:

- User authentication and management
- Product catalog management
- Inventory tracking
- Order processing
- Payment processing
- Notification services
- Event-driven communication
- Containerized deployment
- DevOps automation

The project follows modern, industry-standard architecture patterns:

- Microservices Architecture
- API Gateway Pattern
- Service Discovery
- Database-per-Service Pattern
- REST API Communication
- Event-Driven Architecture
- CI/CD Pipeline

---

## 🏗️ System Architecture

```
                       Client
                         │
                    API Gateway
                         │
   ┌──────────┬──────────┼──────────┐
   │          │          │          │
  User     Product     Order    Inventory
 Service   Service    Service    Service
   │          │          │          │
   DB         DB         DB         DB

                Payment Service
                       │
             Notification Service
                       │
                Kafka Event Broker
```

---

## ✨ Services

### 🔐 User Service

Responsible for user authentication and profile management.

**Features**
- User registration
- User login
- JWT authentication
- Role-based authorization
- Profile management

**Database:** `users_db` (PostgreSQL)

| Column | Type |
|---|---|
| id | PK |
| name | varchar |
| email | varchar |
| password | varchar |
| role | varchar |
| created_date | timestamp |

**APIs**
```
POST /users/register
POST /users/login
GET  /users/{id}
```

---

### 📦 Product Service

Manages product catalog operations.

**Features**
- Create, update, delete products
- Product search
- Product detail lookup

**Example**
```
Product
ID: 101
Name: Laptop
Price: $1200
Category: Electronics
```

**Database:** `product_db` (PostgreSQL)

| Column | Type |
|---|---|
| id | PK |
| name | varchar |
| description | text |
| price | decimal |
| category | varchar |

**APIs**
```
GET  /products
GET  /products/{id}
POST /products
```

---

### 📊 Inventory Service

Handles product stock management.

**Features**
- Stock tracking
- Inventory updates
- Product availability checking
- Low-stock monitoring

**Example**
```
Before purchase → Laptop stock = 10
After purchase  → Laptop stock = 9
```

---

### 🛍️ Order Service

The core business service responsible for order management.

**Features**
- Create orders
- Manage order status
- Track order history
- Order lifecycle management

**Order lifecycle**
```
CREATED → CONFIRMED → PAID → SHIPPED → DELIVERED
```

**Example**
```
Order ID: 5001
Customer: Vihar Patel
Product: Laptop
Status: CONFIRMED
```

---

### 💳 Payment Service

Handles payment processing and transaction records.

**Flow**
```
Order Service → Payment Request → Payment Service
             → Payment Gateway → Payment Successful
```

---

### 📧 Notification Service

Sends customer notifications.

**Supports**
- Email notifications
- Order confirmation
- Payment updates
- Shipping updates

**Architecture**
```
Order Created → Kafka Event → Notification Service → Customer Notification
```

---

## 🌐 API Gateway

The API Gateway acts as the single entry point for all client requests, instead of the frontend calling each service directly.

```
Frontend → API Gateway → User / Product / Order / Inventory Services
```

**Responsibilities**
- Request routing
- Authentication
- Authorization
- Load balancing
- Security filtering

**Technology:** Spring Cloud Gateway

---

## 🔎 Service Discovery — Eureka Server

Microservices register themselves dynamically with Eureka instead of relying on hardcoded URLs.

```
                Eureka Server
              /      │       \
          User    Product    Order
         Service   Service   Service
```

**Benefits**
- Dynamic service discovery
- No hardcoded service URLs
- Easier horizontal scaling

---

## 🔄 Service-to-Service Communication

**Synchronous** — REST API / OpenFeign
```
Order Service → Request Product Details → Product Service → Product Information
```

**Asynchronous** — Apache Kafka
```
Order Created → Kafka Topic → Notification Service
```

**Benefits of async communication**
- Loose coupling
- Higher scalability
- Reliable messaging
- Faster processing

---

## 🗄️ Database Architecture

The project follows the **Database-per-Service** pattern:

| Service | Database |
|---|---|
| User Service | `users_db` |
| Product Service | `product_db` |
| Order Service | `order_db` |

**Advantages**
- Independent scaling
- Better security
- Clear service ownership
- Reduced coupling

---

## 🐳 Docker Deployment

Each microservice runs independently inside its own container.

| Container | Service |
|---|---|
| 1 | API Gateway |
| 2 | User Service |
| 3 | Product Service |
| 4 | Order Service |
| 5 | PostgreSQL |
| 6 | Kafka |

**Run the application**
```bash
docker-compose up
```

---

## 🔐 Security

Implemented using **Spring Security** and **JWT authentication**.

**Authentication flow**
```
Username + Password → Authentication Service → JWT Token → Authorized Request
```

**Example header**
```
Authorization: Bearer <JWT_TOKEN>
```

---

## ⚙️ DevOps Pipeline

```
Developer → GitHub Repository → GitHub Actions → Build & Test
          → Docker Image → Deployment → Cloud Environment
```

**Tools:** GitHub Actions, Docker, Kubernetes, AWS

---

## 📈 Monitoring

- **Spring Boot Actuator** — health checks at `/actuator/health`
- **Prometheus** — collects CPU usage, memory usage, API metrics, and application health
- **Grafana** — dashboards for requests/sec, response time, failed requests, and system health

---

## 🔄 Complete Order Processing Flow

Example: a customer purchases a laptop.

1. Customer places an order
2. Request reaches the API Gateway
3. Product Service validates the product
4. Order Service creates the order
5. Inventory Service updates stock
6. Payment Service processes the payment
7. Kafka publishes an order event
8. Notification Service sends a confirmation email
9. Order is completed successfully

---

## 🛠️ Tech Stack

**Backend**
- Java 17+
- Spring Boot
- Spring Cloud
- Spring Security
- Spring Data JPA
- Hibernate

**Microservices**
- Spring Cloud Gateway
- Eureka Server
- OpenFeign
- Apache Kafka

**Database**
- PostgreSQL

**DevOps**
- Docker / Docker Compose
- GitHub Actions
- Kubernetes

**Monitoring**
- Spring Actuator
- Prometheus
- Grafana

---

## 📂 Project Structure

```
shopx/
├── api-gateway/
├── discovery-server/
├── user-service/
├── product-service/
├── inventory-service/
├── order-service/
├── payment-service/
├── notification-service/
├── docker-compose.yml
└── README.md
```

---

## 🚀 Getting Started

Follow these steps to run **ShopX** locally.

### 📋 Prerequisites

Make sure you have the following installed:

- Java 17+
- Maven 3.9+
- Docker & Docker Compose
- PostgreSQL
- Git

Verify installations:

```bash
java -version
mvn -version
docker --version
docker-compose --version
```

### 📥 Clone Repository

```bash
git clone https://github.com/vihar023/shopx.git
cd shopx
```

### ⚙️ Configure Environment Variables

Create `.env` files for each service and configure:

```bash
DB_USERNAME=postgres
DB_PASSWORD=your_password
JWT_SECRET=your_secret_key
KAFKA_BOOTSTRAP_SERVERS=localhost:9092
```

### 🏗️ Build Microservices

Build all Spring Boot services:

```bash
./mvnw clean install
```

or

```bash
mvn clean install
```

### 🐳 Run Application Using Docker Compose

Start all services:

```bash
docker-compose up --build
```

This will start:

- ✓ API Gateway
- ✓ Eureka Discovery Server
- ✓ User Service
- ✓ Product Service
- ✓ Inventory Service
- ✓ Order Service
- ✓ Payment Service
- ✓ Notification Service
- ✓ PostgreSQL Database
- ✓ Kafka Broker

### 🌐 Access Services

| Service | URL |
|---|---|
| API Gateway | `http://localhost:8080` |
| Eureka Dashboard | `http://localhost:8761` |
| Swagger API Docs | `http://localhost:8080/swagger-ui/index.html` |
| PostgreSQL | `localhost:5432` |
| Kafka | `localhost:9092` |

### 🛑 Stop Application

Stop all running containers:

```bash
docker-compose down
```

Remove containers and volumes:

```bash
docker-compose down -v
```

### 🔍 Verify Running Services

Check Docker containers:

```bash
docker ps
```

Check application health:

```
http://localhost:8080/actuator/health
```

### 📝 Development Workflow

1. Create or update a microservice
2. Run unit tests
3. Build Docker image
4. Start services using Docker Compose
5. Test APIs using Swagger/Postman
6. Commit changes and push to GitHub

---

⭐ If you find this project useful, consider giving it a star!



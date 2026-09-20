# 🏠 Airbnb Platform — Tech Stack

## 1. Frontend

### Next.js

Used for building the web application with server-side and client-side rendering where required.

### React

Used for building reusable and interactive UI components.

### TypeScript

Used for type safety, maintainability, and reliable development across the application.

### Tailwind CSS

Used for responsive, consistent, and scalable UI development.

---

## 2. Backend

### Node.js

Used as the runtime environment for backend services.

### Express.js

Used for building REST APIs and backend services.

### TypeScript

Used across backend services for type-safe development.

---

## 3. API Gateway

An **API Gateway** will act as the primary entry point between the frontend and backend services.

### Responsibilities

* Request routing
* Authentication checks
* Request validation
* Rate limiting
* API protection
* Communication with backend services

Basic flow:

```text
Frontend
   ↓
API Gateway
   ↓
Backend Services
```

---

## 4. Database

### PostgreSQL

PostgreSQL will be the primary relational database.

It will store application data such as:

* Users
* Hosts
* Properties
* Bookings
* Payments
* Reviews
* Wishlists
* Verification records

### Prisma

Prisma ORM will be used for:

* Database access
* Type-safe queries
* Schema management
* Database migrations

The MVP may use a shared PostgreSQL infrastructure while maintaining clear **domain/service boundaries**. These boundaries can later evolve toward independently managed service databases.

---

## 5. Caching & Temporary Data

### Redis

Redis will be used for:

* Frequently accessed data
* Caching
* Session-related data where required
* Temporary data
* Rate limiting
* Availability-related locks where required

---

## 6. Message Broker

### RabbitMQ

RabbitMQ will be used for **asynchronous event-driven communication** between relevant services.

Example events:

```text
UserRegistered
BookingCreated
PaymentCompleted
BookingCancelled
VerificationCompleted
NotificationRequested
```

Basic flow:

```text
Service
   ↓
Event
   ↓
RabbitMQ
   ↓
Consumer Service
```

This reduces unnecessary direct dependency between services.

---

## 7. Search

### OpenSearch / Elasticsearch

A search engine may be introduced as the platform grows.

It can support:

* Fast property search
* Location-based search
* Filtering
* Ranking
* Search suggestions
* AI-assisted search

The initial MVP can use PostgreSQL-based search before introducing a dedicated search engine.

---

## 8. AI Layer

AI capabilities will be introduced from the **MVP** and expanded in later stages.

### MVP

* AI Travel Assistant
* Natural-language property queries
* Basic recommendations
* AI-assisted property information
* Basic guest support

### Major

* Advanced AI Travel Assistant
* AI-powered natural-language search
* Personalized recommendations
* AI Check-in Assistant
* AI customer support
* AI communication assistance
* AI photo authenticity analysis
* Multi-language translation

The AI layer will communicate with the application through dedicated backend services/APIs rather than being tightly coupled to the frontend.

---

## 9. File & Image Storage

### Object Storage

Object storage such as **AWS S3** will be used for:

* Property images
* Verification documents
* Certificates
* Other user-uploaded files

Sensitive documents should be handled through secure access controls and should not be exposed directly as public files.

---

## 10. Containerization

### Docker

Docker will be used to containerize:

* Frontend
* Backend services
* PostgreSQL
* Redis
* RabbitMQ
* Other required infrastructure

### Docker Compose

Docker Compose will be used for:

* Local development
* Running multiple services
* Running infrastructure dependencies
* Local integration testing

---

## 11. Monorepo

### pnpm Workspaces

Used to manage multiple applications, services, and shared packages within a single repository.

### Turborepo

Used for:

* Build management
* Development tasks
* Task orchestration
* Caching
* Dependency management

The project will initially follow a **modular monorepo approach**, with service boundaries designed so important domains can be extracted into independently deployable services as the system grows.

---

## 12. Testing

The project will include:

* Unit Testing
* Integration Testing
* API Testing
* End-to-End Testing

Testing tools will be finalized during implementation.

---

## 13. API Documentation

### OpenAPI / Swagger

OpenAPI will be used to document REST APIs.

Documentation will describe:

* Endpoints
* Request parameters
* Request bodies
* Responses
* Authentication
* Error responses

---

## 14. Monitoring & Logging

The system will progressively introduce:

* Application logging
* Error tracking
* Service health checks
* Metrics
* Monitoring
* Distributed tracing

The complete observability stack will be introduced during the advanced infrastructure phase.

Planned tools include:

* Prometheus
* Grafana
* OpenTelemetry
* Loki / ELK

---

## 15. Deployment

### MVP Deployment

The MVP will have a **basic deployment** so that the application is live and demonstrable.

```text
Development
     ↓
Build
     ↓
Docker / Basic Cloud Deployment
     ↓
Live MVP
```

The focus at this stage will be application functionality rather than large-scale infrastructure.

### Advanced Deployment

The later stages will introduce:

* Kubernetes
* AWS
* Load balancing
* Auto-scaling
* Service orchestration
* Production-grade deployment

---

## 16. CI/CD

### GitHub Actions

GitHub Actions will be used to automate:

* Code checks
* Testing
* Building
* Docker image creation
* Deployment

Basic pipeline:

```text
Git Push
   ↓
CI Pipeline
   ↓
Test
   ↓
Build
   ↓
Docker Image
   ↓
Deployment
```

Advanced stages may introduce more sophisticated deployment strategies and infrastructure automation.

---

# 17. Architecture Style

The project will follow an **incremental architecture strategy**:

```text
Monorepo
   ↓
Modular Backend
   ↓
Clear Domain Boundaries
   ↓
Event-Driven Communication
   ↓
Selected Services Extracted
   ↓
Microservice-Oriented Architecture
   ↓
Containerized Deployment
   ↓
Scalable Production Infrastructure
```

### Core Architecture Principles

* Monorepo architecture
* Modular backend design
* Service/domain boundaries
* REST API architecture
* Event-driven communication where appropriate
* Redis-based caching
* PostgreSQL relational data storage
* Containerized development
* Incremental microservice extraction
* Basic MVP deployment
* Advanced cloud infrastructure
* CI/CD
* Observability

---

# 18. Technology Progression

### MVP / Minor

```text
Next.js
TypeScript
React
Tailwind
Node.js
Express.js
PostgreSQL
Prisma
Redis
RabbitMQ
Docker
Docker Compose
Basic Deployment
AI Assistant
Verification
```

### Major

```text
Advanced AI
Advanced Trust & Fraud
OpenSearch
WebSockets
Advanced Verification
Money Radar
Regulatory Service
Advanced Event Processing
Containerized Services
Scalable Deployment
```

### Advanced / Production

```text
Kubernetes
AWS
Load Balancing
Auto-scaling
CI/CD
Prometheus
Grafana
OpenTelemetry
Loki / ELK
Production Observability
```

---

# 19. Final Technology Stack

```text
                    AIRBNB PLATFORM
                           │
             ┌─────────────┴─────────────┐
             │                           │
         FRONTEND                     BACKEND
             │                           │
      Next.js + React             Node.js + Express
        TypeScript                    TypeScript
        Tailwind CSS                       │
             │                             ▼
             │                       API Gateway
             │                             │
             └──────────────┬──────────────┘
                            │
          ┌─────────────────┼─────────────────┐
          ↓                 ↓                 ↓
     PostgreSQL           Redis            RabbitMQ
       + Prisma          Caching          Event Bus
          │                 │                 │
          └─────────────────┼─────────────────┘
                            ↓
                     Domain Services
                            │
          ┌─────────────────┼─────────────────┐
          ↓                 ↓                 ↓
      Booking          Verification          AI
      Payment           Trust/Fraud       Assistant
      Listing           Property          Search
      Review            Regulatory        Recommendation
          │                 │                 │
          └─────────────────┼─────────────────┘
                            ↓
                    Docker / Containers
                            │
                  ┌─────────┴─────────┐
                  ↓                   ↓
              MVP Deploy         Advanced Deploy
                                      │
                                Kubernetes + AWS
                                      │
                              CI/CD + Monitoring
                                      │
                              Observability Stack
```

---

## 20. Architecture Goal

The technology stack is designed to support the project's progression from a **working Minor/MVP application** to a **Major project with advanced AI and trust capabilities**, and eventually toward a **scalable, observable, production-oriented platform**.

**Core principle:**

> **Build the product first, establish clear architecture boundaries, and progressively introduce distributed infrastructure as the system grows.**

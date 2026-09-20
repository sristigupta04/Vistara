# 🏠 Vistara — Detailed System Architecture

## Day 5 — Service Boundaries, Data Ownership & Communication Design

---

# 1. Architecture Objective

**Vistara** is an AI-powered, trust-aware short-term accommodation platform designed to provide the core functionality of an Airbnb-like marketplace while addressing problems related to:

* Fake identities
* Misleading property information
* Suspicious listings
* Document and certificate inconsistencies
* Business verification
* Fraudulent activity
* Lack of transparency
* Guest-host communication and safety

The architecture is therefore designed around two major layers:

```text
CORE MARKETPLACE
       +
TRUST & INTELLIGENCE LAYER
```

The system will start as a **modular monorepo** and progressively evolve toward a microservice-oriented architecture.

---

# 2. Architecture Principles

Vistara will follow these principles:

* Modular design
* Clear domain boundaries
* Separation of responsibilities
* REST-based synchronous communication
* RabbitMQ-based asynchronous communication
* Central API Gateway
* PostgreSQL for relational data
* Redis for caching and temporary data
* Dedicated AI capabilities
* Verification and trust as first-class domains
* Incremental microservice extraction
* Security by design
* Observability and scalability in later stages

---

# 3. High-Level Architecture

```text
                              ┌──────────────────────┐
                              │       VISTARA        │
                              │      Web App         │
                              │   Next.js + React    │
                              └──────────┬───────────┘
                                         │
                                         ▼
                              ┌──────────────────────┐
                              │     API Gateway      │
                              │ Auth / Routing /     │
                              │ Validation / Limits  │
                              └──────────┬───────────┘
                                         │
              ┌──────────────────────────┼──────────────────────────┐
              │                          │                          │
              ▼                          ▼                          ▼
       ┌─────────────┐            ┌─────────────┐            ┌─────────────┐
       │ Auth / User │            │   Listing   │            │   Search    │
       │   Domain    │            │   Domain    │            │   Domain    │
       └──────┬──────┘            └──────┬──────┘            └──────┬──────┘
              │                          │                          │
              └──────────────────────────┼──────────────────────────┘
                                         │
                                         ▼
                              ┌──────────────────────┐
                              │ Availability/Booking │
                              │       Domain         │
                              └──────────┬───────────┘
                                         │
                       ┌─────────────────┼─────────────────┐
                       ▼                 ▼                 ▼
                ┌─────────────┐  ┌──────────────┐  ┌─────────────┐
                │   Payment   │  │ Verification │  │   Review    │
                │   Domain    │  │    Domain    │  │   Domain    │
                └──────┬──────┘  └───────┬──────┘  └─────────────┘
                       │                 │
                       └────────┬────────┘
                                ▼
                         ┌──────────────┐
                         │  Trust/Risk  │
                         │    Engine    │
                         └──────┬───────┘
                                │
               ┌────────────────┼────────────────┐
               ▼                ▼                ▼
        ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
        │     AI      │  │ Regulatory  │  │Notification │
        │    Layer    │  │   Domain    │  │   Domain    │
        └─────────────┘  └─────────────┘  └─────────────┘

             ┌─────────────────────────────────────┐
             │              RabbitMQ                │
             │          Event Communication        │
             └─────────────────────────────────────┘

             ┌──────────────────┐  ┌──────────────────┐
             │      Redis       │  │   PostgreSQL     │
             │ Cache / Temp     │  │ Relational Data  │
             └──────────────────┘  └──────────────────┘
```

---

# 4. Application Layer

## 4.1 Web Application

The primary user-facing application will be built using:

* Next.js
* React
* TypeScript
* Tailwind CSS

It will provide:

* Property discovery
* Search and filters
* Property details
* Verification information
* Booking
* Payment
* Wishlist
* Reviews
* AI Assistant
* Guest-host communication

---

## 4.2 Admin Application

The Admin Application will provide administrative functionality for:

* User management
* Host management
* Property management
* Verification review
* Suspicious activity review
* Reports
* Booking monitoring
* Platform statistics

---

## 4.3 Host Dashboard

A dedicated host interface will allow hosts to:

* Manage profile
* Complete verification
* Create properties
* Upload documents
* Manage property images
* Manage availability
* Manage pricing
* View bookings
* Track verification status

---

# 5. API Gateway

The API Gateway acts as the entry point for backend requests.

```text
Client
  ↓
API Gateway
  ↓
Required Domain
```

### Responsibilities

* Request routing
* Authentication checks
* Authorization
* Request validation
* Rate limiting
* API protection
* Request logging
* Service communication

The gateway should not contain business logic belonging to individual domains.

---

# 6. Core Domain Services

## 6.1 Auth / User Domain

Responsible for:

* Registration
* Login
* Logout
* Authentication
* Authorization
* Roles
* Sessions/tokens
* User profiles

Roles:

```text
GUEST
HOST
ADMIN
```

---

## 6.2 Listing Domain

Responsible for:

* Property creation
* Property updates
* Property deactivation
* Property information
* Amenities
* Property type
* Capacity
* Location
* Images
* Property rules

---

## 6.3 Search Domain

Responsible for:

* Property search
* Location search
* Filters
* Price filtering
* Amenities
* Ratings
* Availability-aware search
* Search ranking

Later it can integrate with:

```text
OpenSearch / Elasticsearch
```

---

## 6.4 Availability Domain

Responsible for:

* Property availability
* Date management
* Availability checks
* Preventing conflicting reservations
* Availability locks

Redis may be used for temporary locking where appropriate.

---

## 6.5 Booking Domain

Responsible for:

* Creating bookings
* Booking status
* Cancellation
* Booking history
* Reservation lifecycle
* Coordination with availability and payment

Possible states:

```text
PENDING
CONFIRMED
CANCELLED
COMPLETED
```

---

## 6.6 Payment Domain

Responsible for:

* Payment initiation
* Payment verification
* Payment status
* Booking-payment relationship
* Refund status
* Payment failure handling

The payment service should not directly control unrelated property or user data.

---

## 6.7 Review Domain

Responsible for:

* Reviews
* Ratings
* Review eligibility
* Preventing duplicate reviews
* Review moderation

Reviews should be associated with completed bookings.

---

# 7. Verification Domain

Verification is one of the **core differentiating domains of Vistara**.

It is responsible for:

* Identity verification
* Host verification
* Business verification
* Certificate verification
* Document verification
* Property verification
* Verification status
* Verification history

Possible states:

```text
PENDING
VALIDATING
RISK_ANALYSIS
VERIFIED
REJECTED
SUSPICIOUS
```

The verification domain can communicate with external verification sources where legally and technically appropriate.

---

# 8. Trust & Risk Domain

The Trust/Risk Engine analyzes information and activity to identify potential risk indicators.

Possible signals:

* Inconsistent identity information
* Document inconsistencies
* Duplicate property information
* Repeated verification failures
* Suspicious booking patterns
* Multiple reports
* Property information mismatch
* Suspicious account activity

Conceptual flow:

```text
Information
     ↓
Validation
     ↓
Risk Signals
     ↓
Risk Analysis
     ↓
Trust/Risk Result
```

A suspicious indicator should trigger further review rather than automatically declaring a person or property fraudulent.

---

# 9. AI Domain

AI is another major differentiating layer of Vistara.

### MVP

* AI Travel Assistant
* Natural-language property queries
* Basic recommendations
* AI-assisted property information
* Basic guest support

### Major

* Advanced AI Travel Assistant
* AI Search
* Personalized recommendations
* AI Check-in Assistant
* AI customer support
* AI communication assistance
* AI photo authenticity analysis
* Multi-language translation

Architecture:

```text
User
 ↓
API Gateway
 ↓
AI Domain
 ├── Travel Assistant
 ├── AI Search
 ├── Recommendation
 ├── Support
 ├── Check-in Assistant
 └── AI Analysis
```

---

# 10. Regulatory Domain

The Regulatory domain will provide location-based compliance information.

```text
Property
   ↓
Location
   ↓
Applicable Regulations
   ↓
Permit Requirements
   ↓
Tax Requirements
   ↓
Compliance Information
```

Major-stage capabilities may include:

* Regulatory checks
* Permit/status verification
* Compliance risk indicators
* Regulatory change notifications

---

# 11. Notification Domain

The Notification domain handles system-generated notifications.

Examples:

* Registration
* Verification result
* Booking confirmation
* Booking cancellation
* Payment status
* Check-in reminder
* Important account updates

Event-driven flow:

```text
Booking Service
      ↓
BookingCreated
      ↓
RabbitMQ
      ↓
Notification Service
      ↓
Email / Push / SMS
```

---

# 12. Messaging Domain

The Messaging domain will support guest-host communication.

### MVP / Initial

Basic communication capabilities can be implemented using REST APIs.

### Major

Real-time communication can be introduced using:

```text
WebSocket
```

Potential capabilities:

* Guest-host messaging
* Booking-related communication
* AI communication assistance
* Urgent issue escalation
* Check-in communication

---

# 13. Event-Driven Architecture

RabbitMQ will be used where asynchronous communication is beneficial.

Example:

```text
Booking Service
      │
      ▼
BookingCreated Event
      │
      ▼
   RabbitMQ
      │
 ┌────┼───────────────┐
 ▼    ▼               ▼
Payment Notification  Analytics
Service   Service      / Risk
```

Other possible events:

```text
UserRegistered
VerificationSubmitted
VerificationCompleted
BookingCreated
BookingConfirmed
BookingCancelled
PaymentCompleted
ReviewCreated
PropertyReported
RiskDetected
NotificationRequested
```

Not every operation needs RabbitMQ. Direct REST communication will be used when an immediate response is required.

---

# 14. Data Ownership

Vistara will maintain clear ownership of domain data.

| Domain       | Primary Data                                |
| ------------ | ------------------------------------------- |
| Auth/User    | Users, roles, profiles                      |
| Listing      | Properties, amenities, property information |
| Availability | Availability records, reservation locks     |
| Booking      | Reservations, booking status                |
| Payment      | Payment records, transaction status         |
| Review       | Reviews, ratings                            |
| Verification | Verification requests, documents, results   |
| Trust/Risk   | Risk signals, risk assessments              |
| Notification | Notification records                        |
| Regulatory   | Compliance information                      |
| AI           | AI interaction/session data where required  |

### MVP Database Strategy

The MVP may use a common PostgreSQL infrastructure while keeping **logical domain ownership** clear.

### Advanced Strategy

Selected domains can later be extracted into independently deployable services with independently managed data stores where justified.

---

# 15. Redis Usage

Redis will support performance and temporary operations.

Possible uses:

```text
Redis
 ├── API Caching
 ├── Session Data
 ├── Rate Limiting
 ├── Temporary Verification Data
 ├── Availability Locks
 └── Frequently Accessed Data
```

Redis will not be treated as the primary permanent database for core transactional records.

---

# 16. External Integrations

Depending on implementation stage, Vistara may integrate with:

```text
Payment Provider
      │
      ├── Payment Processing

Identity / Verification Sources
      │
      ├── Identity Checks
      ├── Business Verification
      └── Certificate Verification

Maps / Location APIs
      │
      └── Location & Property Search

AI Provider
      │
      └── AI Capabilities

Object Storage
      │
      └── Images / Documents
```

External integrations will be isolated behind appropriate backend modules/services.

---

# 17. Main System Flows

## 17.1 Property Discovery

```text
Guest
 ↓
Web App
 ↓
API Gateway
 ↓
Search Domain
 ↓
Listing / Availability
 ↓
Trust Indicators
 ↓
Property Results
```

---

## 17.2 Booking

```text
Guest
 ↓
Property
 ↓
Availability Check
 ↓
Booking
 ↓
Payment
 ↓
Payment Verification
 ↓
Booking Confirmation
 ↓
RabbitMQ
 ↓
Notification
```

---

## 17.3 Host Verification

```text
Host
 ↓
Submit Information
 ↓
Verification Domain
 ↓
Validation
 ↓
External / Internal Checks
 ↓
Risk Analysis
 ↓
 ┌───────────────┐
 │               │
 ▼               ▼
Low Risk      Higher Risk
 │               │
 ▼               ▼
Verified      Admin Review
                 │
                 ▼
              Decision
```

---

## 17.4 Suspicious Activity

```text
User / Property Activity
          ↓
       Signals
          ↓
    Trust/Risk Engine
          ↓
     Risk Assessment
          ↓
   ┌──────┴──────┐
   ▼             ▼
Normal       Suspicious
                 │
                 ▼
            Admin Review
                 │
                 ▼
              Action
```

---

# 18. Monorepo Architecture

```text
vistara/
│
├── apps/
│   ├── web/
│   ├── admin/
│   └── host-dashboard/
│
├── services/
│   ├── api-gateway/
│   ├── auth/
│   ├── user/
│   ├── listing/
│   ├── search/
│   ├── availability/
│   ├── booking/
│   ├── payment/
│   ├── review/
│   ├── verification/
│   ├── trust-risk/
│   ├── notification/
│   ├── messaging/
│   ├── ai/
│   └── regulatory/
│
├── packages/
│   ├── database/
│   ├── types/
│   ├── validation/
│   ├── auth/
│   ├── config/
│   └── ui/
│
├── infrastructure/
│   ├── docker/
│   ├── rabbitmq/
│   ├── redis/
│   └── monitoring/
│
├── docs/
│   ├── requirements/
│   ├── architecture/
│   ├── api/
│   └── verification/
│
├── docker-compose.yml
├── package.json
├── pnpm-workspace.yaml
└── turbo.json
```

> **Important:** The folder structure defines logical boundaries. All listed services do not need to become independently deployed microservices on Day 1.

---

# 19. Architecture Evolution

Vistara will evolve incrementally.

### Stage 1 — MVP

```text
Monorepo
   ↓
Modular Backend
   ↓
Core Marketplace
   +
AI Assistant
   +
Verification Foundation
   ↓
Basic Deployment
```

### Stage 2 — Major

```text
Modular Architecture
       ↓
Selected Services Extracted
       ↓
Advanced AI
       +
Trust/Risk
       +
Regulatory
       +
Real-Time Communication
```

### Stage 3 — Advanced

```text
Service-Oriented Architecture
        ↓
Docker
        ↓
Kubernetes
        ↓
AWS
        ↓
Auto Scaling
        ↓
CI/CD
        ↓
Observability
```

---

# 20. Day 5 Architecture Decisions

| Decision             | Approach                                        |
| -------------------- | ----------------------------------------------- |
| Frontend             | Next.js + React + TypeScript                    |
| Backend              | Node.js + Express.js + TypeScript               |
| Architecture         | Modular Monorepo → Microservice-oriented        |
| API                  | REST                                            |
| Real-time            | WebSocket in Major stage                        |
| Database             | PostgreSQL + Prisma                             |
| Cache                | Redis                                           |
| Message Broker       | RabbitMQ                                        |
| Search               | PostgreSQL initially → OpenSearch later         |
| AI                   | Dedicated AI domain/service                     |
| Verification         | Dedicated Verification domain                   |
| Trust                | Dedicated Trust/Risk domain                     |
| Storage              | Object Storage / S3                             |
| Local Infrastructure | Docker Compose                                  |
| MVP Deployment       | Basic cloud deployment                          |
| Advanced Deployment  | Kubernetes + AWS                                |
| CI/CD                | GitHub Actions                                  |
| Observability        | Prometheus + Grafana + OpenTelemetry + Loki/ELK |

---

# 21. Day 5 Final Architecture Statement

> **Vistara uses a modular monorepo architecture with clearly separated business domains, REST-based synchronous communication, RabbitMQ-based asynchronous events, PostgreSQL for transactional data, Redis for caching and temporary operations, and dedicated Verification, Trust/Risk, and AI domains. The architecture is designed to evolve progressively from a functional MVP into a scalable, production-oriented platform.**

---

# 22. Architecture Philosophy

The architecture is not designed around creating the maximum number of microservices.

Instead:

```text
BUILD THE CORE
      ↓
DEFINE BOUNDARIES
      ↓
VALIDATE THE SYSTEM
      ↓
EXTRACT WHERE NEEDED
      ↓
SCALE IMPORTANT DOMAINS
      ↓
ADD PRODUCTION INFRASTRUCTURE
```

This allows Vistara to demonstrate both **practical software development** and **advanced system design** without unnecessarily over-engineering the MVP.

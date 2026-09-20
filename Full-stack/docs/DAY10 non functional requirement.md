# Vistara — Day 10: Non-Functional Requirements

> **Building Vistara not only to work, but to work reliably, securely, efficiently, and at scale.**

## 1. Day 10 Objective

Day 10 defines the **Non-Functional Requirements (NFRs)** of Vistara.

Functional requirements define:

> **What the system does**

Non-functional requirements define:

> **How well the system should do it**

For Vistara, the major quality attributes are:

```text
Performance
Security
Scalability
Availability
Reliability
Maintainability
Usability
Observability
Data Integrity
AI Performance
API Quality
Deployment
```

---

# 2. NFR Categories

```text
                    VISTARA NFR
                         │
       ┌─────────────────┼─────────────────┐
       ↓                 ↓                 ↓
   PERFORMANCE        SECURITY        RELIABILITY
       │                 │                 │
       ├── Latency       ├── Auth          ├── Fault Handling
       ├── Throughput    ├── RBAC          ├── Recovery
       └── Caching       └── Data Safety   └── Consistency

       ┌─────────────────┼─────────────────┐
       ↓                 ↓                 ↓
   SCALABILITY       MAINTAINABILITY   OBSERVABILITY
       │                 │                 │
       ├── Redis         ├── Modular Code  ├── Logs
       ├── Docker        ├── Testing       ├── Metrics
       └── Instances     └── Documentation └── Monitoring
```

---

# 3. Performance Requirements

## NFR-PERF-01 — Page Response

The application should provide responsive page loading under normal conditions.

Target:

```text
Common UI/API operations
        ↓
Fast response
        ↓
No unnecessary blocking
```

Heavy operations such as AI processing, verification processing, and asynchronous tasks should not unnecessarily block the main request.

---

## NFR-PERF-02 — API Response

Core APIs should target approximately:

```text
Normal CRUD APIs
→ < 500 ms target

Search APIs
→ < 1 second target

Complex / AI operations
→ asynchronous or streamed where appropriate
```

These are **development targets**, not guarantees.

---

## NFR-PERF-03 — Database Performance

Database queries should:

* Use appropriate indexes
* Avoid unnecessary data retrieval
* Use pagination
* Avoid N+1 query patterns
* Return only required fields where practical

Important entities include:

```text
User
Property
Booking
Review
Verification
Payment
```

---

# 4. Search Performance

## NFR-SEARCH-01

Search should remain responsive as the number of properties increases.

Search operations should use:

```text
Indexes
+
Pagination
+
Filtering
+
Caching where useful
```

Major phase may introduce:

```text
OpenSearch / Elasticsearch
```

for more advanced search requirements.

---

# 5. AI Performance

## NFR-AI-01 — AI Response

AI interactions should provide a responsive experience.

For longer AI operations, the UI should communicate state:

```text
Thinking...
     ↓
Processing...
     ↓
Result
```

rather than appearing frozen.

---

## NFR-AI-02 — AI Timeout

AI requests must have appropriate timeout and failure handling.

Example:

```text
AI Request
    ↓
Timeout?
 ┌──┴──┐
Yes   No
 ↓     ↓
Fallback Result
```

---

## NFR-AI-03 — AI Graceful Degradation

If the AI service is unavailable:

```text
AI unavailable
      ↓
Normal search still works
```

AI should enhance the marketplace, not make the basic marketplace unusable.

---

# 6. Security Requirements

Security is a core requirement because Vistara handles:

* User accounts
* Identity information
* Property information
* Bookings
* Payments
* Verification information
* Reviews
* Trust signals

---

## NFR-SEC-01 — Authentication Security

Authentication must use secure practices.

Requirements include:

* Password hashing
* Secure sessions/tokens
* Protected routes
* Secure credential handling
* Authentication validation

---

## NFR-SEC-02 — Authorization

Role-based authorization must be enforced on the backend.

```text
Guest
  ↓
Guest APIs

Host
  ↓
Host APIs

Admin
  ↓
Admin APIs
```

Frontend hiding alone is not considered sufficient security.

---

## NFR-SEC-03 — Input Validation

User-controlled input must be validated before processing.

Examples:

```text
Registration
Property Data
Booking Data
Reviews
Requirements
Search Queries
AI Input
```

---

## NFR-SEC-04 — Sensitive Data Protection

Sensitive information should:

* Not be exposed unnecessarily
* Not appear in normal logs
* Be protected during transmission
* Have restricted access

---

## NFR-SEC-05 — API Security

APIs should use:

* Authentication
* Authorization
* Input validation
* Rate limiting where appropriate
* Secure error handling

---

# 7. Rate Limiting

## NFR-SEC-06

Public or abuse-sensitive endpoints should support rate limiting.

Especially:

```text
Login
Registration
Search
AI Requests
Verification
Reports
```

Redis can be used for distributed rate limiting.

```text
Request
   ↓
Rate Limit Check
   ↓
Redis
   ↓
Allow / Reject
```

---

# 8. Data Integrity

## NFR-DATA-01

Important relationships must remain consistent.

Examples:

```text
User
 ↓
Booking
 ↓
Payment
```

```text
Property
 ↓
Booking
 ↓
Review
```

```text
Property
 ↓
Verification
 ↓
Trust Signal
```

---

## NFR-DATA-02 — Booking Consistency

The system must avoid double booking.

Conceptually:

```text
Check Availability
       ↓
Reservation Process
       ↓
Atomic / Protected Booking Operation
       ↓
Booking Confirmed
```

The exact implementation will be determined during backend development.

---

# 9. Reliability

## NFR-REL-01 — Fault Handling

A failure in one non-critical subsystem should not unnecessarily bring down the entire application.

Example:

```text
AI Service ❌
     ↓
Marketplace ✓
     ↓
Normal Search ✓
```

---

## NFR-REL-02 — External Service Failure

External services such as:

* Payment provider
* Email provider
* AI provider
* Verification provider

should have appropriate error handling.

---

## NFR-REL-03 — Retry

Retry mechanisms may be used for appropriate transient operations.

Example:

```text
Notification
     ↓
Failed
     ↓
Retry
     ↓
Success
```

Retries must avoid creating duplicate bookings or payments.

---

# 10. Availability

## NFR-AVAIL-01

The core marketplace should remain available even when optional features experience temporary failure.

Priority:

```text
Authentication
      ↓
Property Discovery
      ↓
Booking
      ↓
Payment
```

These are more critical than optional AI functionality.

---

# 11. Scalability

Vistara should be designed so that the system can scale without requiring the Minor project to purchase expensive infrastructure.

## NFR-SCALE-01 — Horizontal Scaling

Backend should be designed to support multiple instances.

```text
                Load Balancer
                 /    |    \
                /     |     \
             API-1  API-2  API-3
                \     |     /
                 \    |    /
                  Database
```

---

## NFR-SCALE-02 — Stateless Backend

Where practical, application instances should remain stateless.

Shared state should be handled through systems such as:

```text
PostgreSQL
Redis
Object Storage
```

---

## NFR-SCALE-03 — Redis

Redis can support:

* Caching
* Sessions where applicable
* Rate limiting
* Temporary data
* Frequently accessed information

---

## NFR-SCALE-04 — RabbitMQ

RabbitMQ can handle asynchronous operations such as:

```text
Booking Event
     ↓
RabbitMQ
     ├── Notification
     ├── Email
     ├── Analytics
     └── Other Async Tasks
```

This reduces unnecessary work inside synchronous requests.

---

# 12. Scalability Demonstration — Minor

The Minor project does not require expensive cloud infrastructure.

Instead, scalability can be demonstrated locally using:

```text
Docker
+
Multiple Backend Instances
+
API Gateway
+
Redis
+
RabbitMQ
```

Example:

```text
                 API Gateway
                     │
          ┌──────────┼──────────┐
          ↓          ↓          ↓
       Server 1   Server 2   Server 3
          │          │          │
          └──────────┼──────────┘
                     ↓
                   Redis
                     +
                 PostgreSQL
                     +
                 RabbitMQ
```

This demonstrates that the architecture can evolve toward larger deployments.

---

# 13. Maintainability

## NFR-MAINT-01 — Modular Architecture

Code should be organized by clear domain boundaries.

Example:

```text
auth
users
properties
bookings
payments
reviews
verification
trust
ai
notifications
admin
```

---

## NFR-MAINT-02 — Separation of Concerns

The system should separate:

```text
UI
 ↓
API
 ↓
Business Logic
 ↓
Data Access
 ↓
Database
```

---

## NFR-MAINT-03 — Reusable Components

Frontend should use reusable components.

```text
PropertyCard
ReviewCard
TrustCard
VerificationBadge
BookingCard
PriceBreakdown
```

---

# 14. Code Quality

## NFR-CODE-01

Development should follow:

* TypeScript where applicable
* Consistent naming
* Reusable functions
* Clear folder structure
* Environment-based configuration
* Error handling
* Documentation

---

# 15. Testing Requirements

## NFR-TEST-01

The project should include testing at multiple levels.

```text
Unit Tests
    ↓
Integration Tests
    ↓
API Tests
    ↓
Frontend Tests
    ↓
End-to-End Tests
```

---

## NFR-TEST-02 — Critical Flows

Critical flows should receive higher testing priority.

```text
Registration
Login
Property Creation
Search
Availability
Booking
Payment
Verification
Review
Requirement Confirmation
```

---

# 16. API Quality

## NFR-API-01 — REST API Standards

APIs should follow consistent REST conventions.

Example:

```text
GET    /properties
GET    /properties/:id
POST   /properties
PUT    /properties/:id
DELETE /properties/:id
```

---

## NFR-API-02 — Error Format

API errors should use a consistent structure.

Example:

```json
{
  "success": false,
  "message": "Property not found",
  "code": "PROPERTY_NOT_FOUND"
}
```

---

## NFR-API-03 — API Documentation

Core APIs should be documented using:

```text
OpenAPI
Swagger
```

---

# 17. Observability

The system should provide enough information to understand failures and performance.

## NFR-OBS-01 — Logging

Logs should capture relevant events such as:

```text
Request
Error
Authentication Event
Booking Event
Payment Event
Verification Event
AI Request
System Event
```

Sensitive information such as passwords, authentication secrets, and unnecessary identity data must not be written to logs.

---

## NFR-OBS-02 — Error Tracking

Application errors should be identifiable with useful context.

Example:

```text
Request
   ↓
Error
   ↓
Error ID / Context
   ↓
Log
   ↓
Debugging
```

The system should avoid exposing internal stack traces or sensitive implementation details to normal users.

---

## NFR-OBS-03 — Metrics

The system should track useful operational metrics such as:

* API response time
* Request count
* Error rate
* Booking count
* Payment failures
* AI request count
* AI failure rate
* Queue activity
* Database performance where practical

---

## NFR-OBS-04 — Health Checks

Core services should provide health information.

Example:

```text
/api/health

Application       ✓
Database          ✓
Redis             ✓
RabbitMQ          ✓
```

A dependency failure should be identifiable separately from an application failure where possible.

---

# 18. Usability

## NFR-USE-01 — Simple Navigation

Users should be able to understand the primary navigation without unnecessary complexity.

```text
Stay
Explore
Experiences
Services
Search
Wishlist
Trips
Profile
```

---

## NFR-USE-02 — Clear Information Hierarchy

Important information should be easy to find.

Priority:

```text
Property
   ↓
Price
   ↓
Availability
   ↓
Trust
   ↓
Requirements
   ↓
Reviews
   ↓
Booking
```

---

## NFR-USE-03 — Clear Trust Communication

Verification information must be understandable.

Example:

```text
✓ Verified
⏳ Verification in Progress
⚠ Review Required
✕ Verification Rejected
```

The system should not use confusing or unnecessarily alarming language.

---

## NFR-USE-04 — Booking Clarity

Before confirming a booking, the user should clearly understand:

* Property
* Dates
* Guests
* Price
* Requirements
* Cancellation information where applicable
* Payment status

---

# 19. Accessibility

## NFR-ACCESS-01

The interface should aim to support accessible interaction.

Considerations include:

* Readable typography
* Sufficient contrast
* Keyboard navigation
* Semantic HTML
* Descriptive labels
* Alternative text for important images
* Accessible form controls
* Clear error messages

---

## NFR-ACCESS-02 — Responsive Accessibility

Important functionality should remain usable across:

```text
Mobile
Tablet
Desktop
```

---

# 20. Responsive Design

## NFR-RESP-01

The application must support responsive layouts.

### Mobile

```text
Single-column
↓
Simplified navigation
↓
Stacked information
↓
Sticky / accessible booking action
```

### Desktop

```text
Navigation
      ↓
Large Gallery
      ↓
Content + Booking Panel
```

---

# 21. Data Privacy

## NFR-PRIV-01

User information should only be collected and processed when required for the relevant functionality.

---

## NFR-PRIV-02

Access to sensitive verification information should be restricted according to role and system requirements.

```text
Guest
  ↓
Limited Relevant Information

Host
  ↓
Own Relevant Information

Admin
  ↓
Authorized Verification Information
```

---

## NFR-PRIV-03

The system should avoid unnecessarily exposing:

* Passwords
* Authentication tokens
* Sensitive identity information
* Internal verification data
* Payment credentials

---

# 22. Data Consistency

## NFR-DATA-03 — Transaction Consistency

Important operations should maintain consistent database state.

Examples:

```text
Booking + Availability
Booking + Payment
Property + Verification
Booking + Review
```

---

## NFR-DATA-04 — Referential Integrity

Database relationships must remain valid.

Example:

```text
USER
 ↓
BOOKING
 ↓
PROPERTY
 ↓
REVIEW
```

Records should not create invalid relationships.

---

# 23. Caching

## NFR-CACHE-01

Frequently accessed, relatively stable information may be cached.

Possible candidates:

```text
Popular Properties
Property Metadata
Search Results
Destination Information
Session Data
Rate Limits
```

Redis may be used for this purpose.

---

## NFR-CACHE-02 — Cache Invalidation

Data that can change frequently must not remain stale indefinitely.

Examples:

```text
Availability
Booking Status
Payment Status
Verification Status
```

These should have appropriate cache strategies or bypass caching when necessary.

---

# 24. Asynchronous Processing

## NFR-ASYNC-01

Long-running or non-critical tasks should be moved away from synchronous request processing where appropriate.

Example:

```text
Booking Created
      ↓
RabbitMQ
      ├── Email
      ├── Notification
      ├── Analytics
      └── Other Background Tasks
```

This helps keep user-facing requests responsive.

---

## NFR-ASYNC-02 — Event Reliability

Important asynchronous events should be handled in a way that reduces:

* Lost events
* Duplicate processing
* Unhandled failures

---

# 25. Deployment Requirements

## NFR-DEPLOY-01 — Containerization

Services should be containerizable using Docker.

Example:

```text
Docker
 │
 ├── Frontend
 ├── Backend
 ├── PostgreSQL
 ├── Redis
 └── RabbitMQ
```

---

## NFR-DEPLOY-02 — Environment Configuration

Environment-specific configuration must not be hardcoded.

Examples:

```text
Database URL
API Keys
JWT / Auth Secrets
Payment Configuration
AI Provider Configuration
Redis URL
RabbitMQ URL
```

Use environment variables or secure configuration mechanisms.

---

## NFR-DEPLOY-03 — Local Development

The complete Minor system should be runnable locally using appropriate development tooling.

Docker Compose can be used to simplify infrastructure setup.

---

# 26. Backup & Recovery

## NFR-REC-01

Important persistent data should have a backup strategy appropriate to the deployment environment.

Important data includes:

```text
Users
Properties
Bookings
Payments
Reviews
Verification Records
```

---

## NFR-REC-02 — Recovery

The system should have a documented approach for recovering from:

* Application failure
* Database failure
* Infrastructure restart
* Temporary service failure

The exact production recovery targets can be defined during the Major phase.

---

# 27. Configuration Management

## NFR-CONFIG-01

Configuration should be separated from application code.

Example:

```text
Development
    ↓
Environment Configuration

Testing
    ↓
Environment Configuration

Production
    ↓
Environment Configuration
```

---

# 28. API Reliability

## NFR-API-04

APIs should handle invalid requests gracefully.

```text
Invalid Request
      ↓
Validation
      ↓
400 / Appropriate Error
```

---

## NFR-API-05

APIs should return predictable response structures.

Example:

```json
{
  "success": true,
  "data": {}
}
```

or:

```json
{
  "success": false,
  "message": "Something went wrong",
  "code": "ERROR_CODE"
}
```

---

# 29. API Versioning

## NFR-API-06

The API should be structured so that future changes can be introduced without unnecessarily breaking existing clients.

Possible structure:

```text
/api/v1/...
```

Versioning strategy can evolve as the system grows.

---

# 30. Security of Verification System

Verification is one of Vistara's sensitive domains.

## NFR-VERIFY-SEC-01

Verification information should have restricted access.

```text
Verification Data
       ↓
Access Control
       ↓
Authorized Users / Admin
```

---

## NFR-VERIFY-SEC-02

Verification results should not expose unnecessary underlying sensitive information to ordinary users.

Users generally need the result:

```text
✓ Verified
⏳ Pending
⚠ Review Required
✕ Rejected
```

rather than the complete internal verification data.

---

# 31. Payment Security

## NFR-PAY-SEC-01

Payment processing should avoid storing sensitive payment credentials unnecessarily.

Where possible, payment processing should use a trusted payment provider.

---

## NFR-PAY-SEC-02

Payment status must be validated before marking a booking as successfully paid.

```text
Payment Request
      ↓
Payment Provider
      ↓
Payment Result
      ↓
Validation
      ↓
Booking Payment Status
```

---

# 32. Review Integrity

## NFR-REVIEW-01

The system should maintain the relationship between reviews and eligible stays.

Conceptually:

```text
Completed Booking
       ↓
Eligible Review
       ↓
Review
       ↓
Property
```

This supports the **Verified Stay** concept.

---

## NFR-REVIEW-02

Review content should be handled through appropriate validation and moderation mechanisms.

Advanced review anomaly detection belongs to the Major phase.

---

# 33. AI Reliability & Safety

## NFR-AI-04

AI output should not directly modify critical booking or payment information without appropriate application-level validation.

```text
AI Output
   ↓
Application Validation
   ↓
Business Rules
   ↓
Action
```

---

## NFR-AI-05

AI should not be treated as the authoritative source for verification decisions.

Verification status should come from the defined verification workflow.

---

## NFR-AI-06 — AI Fallback

If AI becomes unavailable:

```text
AI ❌
 ↓
Normal Search ✓
 ↓
Normal Booking ✓
```

The core marketplace should continue functioning.

---

# 34. Internationalization Readiness

The initial Minor implementation may focus on the primary target market, but the system should avoid unnecessarily hardcoding language-specific assumptions.

Future support can include:

```text
Language
Currency
Date Format
Time Format
Location Format
```

Advanced internationalization can be expanded in the Major phase.

---

# 35. Performance Under Load

The application should be tested with increasing numbers of:

```text
Users
Properties
Search Requests
Bookings
Reviews
AI Requests
```

Conceptually:

```text
100 Users
   ↓
1,000 Users
   ↓
10,000 Users
   ↓
Higher Load
```

The purpose is to identify bottlenecks before production scaling.

---

# 36. Scalability Architecture

The system should be designed for gradual growth.

```text
                    API Gateway
                         │
             ┌───────────┼───────────┐
             ↓           ↓           ↓
          API-1        API-2       API-3
             │           │           │
             └───────────┼───────────┘
                         ↓
                    PostgreSQL
                         │
              ┌──────────┴──────────┐
              ↓                     ↓
            Redis                RabbitMQ
```

Minor demonstrates the concept.

Major can extend it into:

```text
Microservices
+
Kubernetes
+
Cloud Infrastructure
+
Auto Scaling
+
Advanced Observability
```

---

# 37. Maintainability & Extensibility

Vistara should be designed so that new domains can be added without rewriting the entire application.

Current domains:

```text
Auth
Users
Properties
Search
Bookings
Payments
Reviews
Verification
Trust
AI
Experiences
Services
Notifications
Admin
```

Future domains:

```text
Money Radar
Regulatory
Messaging
Travel Agency
Tourism Marketplace
Advanced AI
```

---

# 38. Technology Alignment

The NFRs should align with the planned architecture.

| Requirement       | Technology / Approach                   |
| ----------------- | --------------------------------------- |
| Database          | PostgreSQL                              |
| ORM               | Prisma                                  |
| Caching           | Redis                                   |
| Async Processing  | RabbitMQ                                |
| API               | Node.js + Express                       |
| Frontend          | Next.js + React                         |
| Type Safety       | TypeScript                              |
| Containerization  | Docker                                  |
| API Documentation | OpenAPI / Swagger                       |
| Testing           | Unit + Integration + E2E                |
| Search            | Database Search → Advanced Search later |
| AI                | Dedicated AI Layer                      |
| Storage           | Object Storage                          |
| Deployment        | Basic deployment → Cloud later          |

---

# 39. Minor NFR Scope

The Minor project should demonstrate:

```text
✓ Responsive UI
✓ Secure authentication
✓ Role-based authorization
✓ Input validation
✓ PostgreSQL data integrity
✓ API error handling
✓ Redis caching / rate limiting
✓ RabbitMQ asynchronous processing
✓ Docker
✓ Basic logging
✓ Health checks
✓ API documentation
✓ Testing
✓ Basic deployment
✓ Multiple-instance scalability demonstration
✓ AI fallback
```

---

# 40. Major NFR Scope

The Major phase can extend the system with:

```text
→ Advanced scalability
→ Kubernetes
→ AWS
→ Auto Scaling
→ Load Balancing
→ Service Discovery
→ Advanced Message Infrastructure
→ OpenSearch / Elasticsearch
→ Advanced Monitoring
→ Prometheus
→ Grafana
→ OpenTelemetry
→ Centralized Logging
→ Advanced CI/CD
→ Infrastructure as Code
→ Advanced Disaster Recovery
```

---

# 41. NFR Priority

Not every requirement has the same implementation priority.

### Critical

```text
Security
Data Integrity
Booking Consistency
Authentication
Authorization
Payment Reliability
Core Availability
```

### High

```text
Performance
Scalability
Reliability
Testing
Observability
Maintainability
```

### Supporting

```text
Accessibility
Internationalization Readiness
Advanced Monitoring
Advanced Infrastructure
```

---

# 42. NFR Acceptance Perspective

The system should be considered ready for the next development phase when:

```text
Security
      ✓
Performance Targets
      ✓
Data Integrity
      ✓
Error Handling
      ✓
Scalability Design
      ✓
Testing Strategy
      ✓
Logging
      ✓
Deployment Strategy
      ✓
AI Fallback
      ✓
```

The targets are treated as **engineering goals**, and actual performance will be validated through testing rather than assumed.

---

# 43. Day 10 Final Architecture Principle

Vistara is not designed only to answer:

> **"Does it work?"**

It must also answer:

> **"Does it remain secure, reliable, maintainable, observable, and scalable as the system grows?"**

Therefore:

```text
FUNCTIONAL REQUIREMENTS
          +
NON-FUNCTIONAL REQUIREMENTS
          ↓
       VISTARA
          ↓
Reliable Product
          ↓
Scalable Architecture
          ↓
Major / Production Evolution
```

---

# 44. Final Day 10 Outcome

Day 10 establishes the engineering quality standards for Vistara.

The final NFR framework is:

```text
                    VISTARA
                       │
 ┌──────────┬──────────┼──────────┬──────────┐
 ↓          ↓          ↓          ↓          ↓
Security Performance Reliability Scalability Maintainability
 │          │          │          │          │
 ↓          ↓          ↓          ↓          ↓
Privacy    Latency    Recovery    Redis       Modular
Auth       Throughput Fault       RabbitMQ    Testing
RBAC       Caching   Handling    Docker      Documentation
Validation DB        Availability Instances   Extensibility

                       │
              ┌────────┴────────┐
              ↓                 ↓
         Observability         AI
              │                 │
           Logs              Latency
           Metrics           Fallback
           Health            Reliability
           Errors            Validation

                       ↓
                 Production Ready
                       ↓
                 Major Evolution
```

---

# 45. Day 10 Completion Checklist

```text
[✓] Performance Requirements
[✓] Search Performance
[✓] AI Performance
[✓] Security
[✓] Authentication Security
[✓] Authorization
[✓] Input Validation
[✓] Rate Limiting
[✓] Data Integrity
[✓] Booking Consistency
[✓] Reliability
[✓] Availability
[✓] Scalability
[✓] Redis
[✓] RabbitMQ
[✓] Maintainability
[✓] Code Quality
[✓] Testing
[✓] API Standards
[✓] OpenAPI / Swagger
[✓] Logging
[✓] Metrics
[✓] Health Checks
[✓] Usability
[✓] Accessibility
[✓] Responsive Design
[✓] Data Privacy
[✓] Caching
[✓] Async Processing
[✓] Docker
[✓] Deployment
[✓] Backup & Recovery
[✓] Verification Security
[✓] Payment Security
[✓] Review Integrity
[✓] AI Reliability
[✓] Scalability Demonstration
[✓] Minor / Major NFR Split
```

---

# Final Statement

> **Day 10 defines the quality contract of Vistara.**

Day 9 defined **what Vistara does**.

Day 10 defines **how reliably, securely, efficiently, and sustainably Vistara should do it**.

```text
Day 9
WHAT THE SYSTEM DOES
        +
Day 10
HOW THE SYSTEM SHOULD PERFORM
        ↓
Complete Functional + Quality Foundation
        ↓
Day 11 — ML Research
```

**Day 10 Complete.**

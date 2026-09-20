# Vistara — Day 8: MVP & Project Scope Definition

## Phase 1 — MVP, Minor & Major Scope Freeze

---

## 1. Objective

Day 8 focuses on defining and freezing the implementation scope of Vistara.

The objective is to clearly separate:

* Features that will be fully implemented in the **Minor Project**
* Features that will be developed as part of the **Major Project**
* Features that are intentionally postponed until the later stages of the project

The Minor Project will not be limited to a basic CRUD accommodation application. It will provide a complete working marketplace with AI capabilities, trust and verification features, experiences, services, dashboards, deployment, and a practical demonstration of scalable architecture.

The Major Project will extend this foundation with advanced AI, advanced trust and risk intelligence, financial transparency, regulatory capabilities, real-time communication, broader tourism services, and deeper scalability.

---

# 2. Vistara Product Vision

Vistara is designed as a trust-aware and AI-enabled accommodation and travel marketplace.

The long-term product evolution is:

```text
Accommodation
      ↓
Experiences
      ↓
Services
      ↓
Travel
      ↓
Broader Tourism Ecosystem
```

The implementation will follow a staged approach instead of attempting to build the entire ecosystem at once.

```text
                    VISTARA
                       │
              ┌────────┴────────┐
              ↓                 ↓
           MINOR              MAJOR
       Working Product    Advanced Product
```

---

# 3. Minor Project Definition

The Minor Project will deliver a functional and deployable Vistara platform.

It will include:

1. Accommodation marketplace
2. Experiences
3. Basic services
4. Search and discovery
5. Booking and payment
6. Reviews and ratings
7. Trust and verification
8. Host requirements
9. Guest requirement confirmation
10. Post-stay mismatch reporting
11. AI-assisted discovery
12. AI assistant
13. Basic recommendation
14. Guest, Host and Admin dashboards
15. Notifications
16. Basic price transparency
17. Testing
18. Docker-based development
19. Redis and RabbitMQ usage
20. Scalability demonstration
21. Basic deployment

---

# 4. Accommodation Marketplace

Accommodation is the primary marketplace of the Minor Project.

## Supported Property Categories

The following categories will be available:

* Hotel
* Apartment
* Villa
* Homestay
* Hostel
* Resort
* Cottage
* Cabin
* Guest House
* Farm Stay
* Beach House
* Luxury Home

Users will be able to discover properties through these categories.

Hosts will select an appropriate category while creating a property.

---

# 5. Property Management

Hosts will be able to manage their properties through a dedicated dashboard.

### Host Capabilities

* Create property
* Edit property
* Delete property
* Upload multiple images
* Add property description
* Set location
* Set price
* Select property category
* Add amenities
* Set maximum guest capacity
* Set availability
* Add house rules
* Define host requirements
* Manage listing status

### Property Details

The property page will provide:

* Property images
* Property name
* Location
* Price
* Description
* Amenities
* Guest capacity
* Availability
* Reviews
* Host information
* Verification information
* Host requirements
* Trust indicators

---

# 6. Search & Discovery

Vistara will provide a complete property discovery experience.

## Search Parameters

Users can search using:

* Location
* Check-in date
* Check-out date
* Number of guests

## Filters

* Price range
* Property category
* Rating
* Amenities
* Verification status
* Pet-friendly
* Parking
* Guest capacity
* Availability

## Sorting

* Price
* Rating
* Relevance
* Recommended
* Newest

## Map-Based Discovery

Properties will also be discoverable through a map interface.

---

# 7. AI Features — Minor

AI is a core part of the Minor Project rather than a future-only feature.

## 7.1 AI Travel Assistant

Users will be able to interact with Vistara using natural language.

Example:

> "Find me a verified villa in North Goa for four people, with parking and pets allowed, under ₹5,000."

The system can process:

```text
User Query
     ↓
Natural Language Understanding
     ↓
Requirement Extraction
     ↓
Location
Budget
Guests
Property Type
Amenities
Trust Requirements
     ↓
Property Search
     ↓
Filtering
     ↓
Recommendation
```

---

# 8. Natural Language Search

Users will not always need to manually select every filter.

Example:

> "Affordable family homestay near the beach with parking."

The AI layer can convert the query into structured search parameters:

```text
Location      → Beach area
Property Type → Homestay
User Type     → Family
Amenity       → Parking
Budget        → Affordable
```

The structured requirements will then be passed to the search system.

---

# 9. Basic AI Recommendation

The Minor Project will include an initial recommendation system.

Possible signals include:

* Search history
* Viewed properties
* Wishlist
* Budget
* Location
* Property category
* Amenities
* Previous bookings
* Ratings

Basic flow:

```text
User Behaviour
      ↓
Preference Identification
      ↓
Property Matching
      ↓
Recommendation
```

The initial implementation may use rule-based or content-based techniques.

Advanced ML recommendation will be part of the Major Project.

---

# 10. AI-Assisted Support

The Minor AI layer can also assist users with:

* Property-related questions
* Booking-related questions
* Host requirements
* Basic travel questions
* Platform navigation
* General support

More advanced AI support will be developed in the Major Project.

---

# 11. Trust & Verification

Trust is a core part of the Vistara product.

The Minor Project will establish the foundation for:

* Identity verification
* Host verification
* Business verification
* Property verification
* Certificate/document verification

## Verification Lifecycle

```text
PENDING
   ↓
VALIDATING
   ↓
VERIFIED
   /
REJECTED
   /
REVIEW REQUIRED
```

`Review Required` or `Suspicious` status indicates that additional investigation may be required. It does not automatically establish fraud.

---

# 12. Trust Indicators

Relevant verification information can be displayed on host and property pages.

Example:

```text
✓ Identity Verified
✓ Property Information Checked
✓ Business Information Checked
✓ Documents Checked
```

This provides users with more context while evaluating a property.

---

# 13. Host Requirements

Hosts will be able to define requirements before accepting bookings.

Possible requirements include:

* Maximum number of guests
* ID requirement
* Age-related requirements where applicable
* Pet policy
* Smoking policy
* Check-in rules
* Check-out rules
* House rules
* Required documents where applicable
* Property-specific requirements

---

# 14. Guest Requirement Confirmation

Before completing a booking, the guest will see the host's requirements.

The guest must explicitly confirm:

```text
☑ I have read and agree to the host requirements.
```

Flow:

```text
Host Defines Requirements
          ↓
Guest Views Requirements
          ↓
Guest Confirms
          ↓
Booking
```

---

# 15. Requirement Snapshot

At the time of booking, the agreed requirements will be stored as a snapshot.

```text
Host Requirements
        ↓
Requirement Snapshot
        ↓
Booking Record
```

This ensures that the requirements associated with an existing booking remain historically traceable even if the host later changes the property requirements.

---

# 16. Post-Stay Mismatch Reporting

Vistara will connect the booking experience with post-stay trust feedback.

```text
Listing / Host Claim
        ↓
Booking
        ↓
Actual Stay
        ↓
Guest Experience
        ↓
Match / Mismatch
        ↓
Review / Report
        ↓
Trust System
```

Guests can report significant issues such as:

* Listing mismatch
* Property mismatch
* Amenity mismatch
* Host requirement mismatch
* Significant property condition issue

The report can be reviewed by administrators.

---

# 17. Vistara Trust Loop

The complete Minor trust workflow is:

```text
             HOST CLAIM
                  ↓
             VERIFICATION
                  ↓
                BOOKING
                  ↓
                 STAY
                  ↓
          ACTUAL EXPERIENCE
                  ↓
          ┌───────┴───────┐
          ↓               ↓
        MATCH          MISMATCH
          ↓               ↓
       REVIEW           REPORT
          │               │
          └───────┬───────┘
                  ↓
             TRUST SIGNAL
                  ↓
             ADMIN REVIEW
```

This creates a feedback loop rather than treating verification as a one-time badge.

---

# 18. Booking & Payment

## Booking

* Date selection
* Availability validation
* Guest details
* Requirement confirmation
* Booking creation
* Booking cancellation
* Booking status
* Booking history

## Payment

* Basic online payment
* Payment status
* Failed payment handling
* Booking-payment relationship

---

# 19. Basic Price Transparency

The complete Money Radar will remain part of the Major Project.

However, the Minor Project will provide a basic cost breakdown.

Example:

```text
Base Price          ₹4,000
Cleaning Fee          ₹500
Taxes                 ₹810
────────────────────────
Estimated Total      ₹5,310
```

This gives users a clearer understanding of the expected booking cost.

---

# 20. Wishlist

Users will be able to:

* Add properties to wishlist
* Remove properties
* View saved properties
* Use wishlist behaviour as a recommendation signal

---

# 21. Reviews & Ratings

Guests can provide reviews after eligible stays.

Review dimensions can include:

* Overall experience
* Cleanliness
* Location
* Communication
* Check-in
* Property accuracy
* Written review

Basic AI-assisted review classification may also be used to identify common themes such as:

```text
Cleanliness
Location
Communication
Check-in
Property Accuracy
```

Advanced review anomaly detection will be part of the Major Project.

---

# 22. Experiences — Minor

Vistara will also provide a basic Experiences marketplace.

Examples:

* Local food experiences
* City tours
* Photography walks
* Adventure activities
* Cultural experiences
* Workshops
* Nature experiences
* Local guides

Experience providers can:

* Create experiences
* Add descriptions
* Upload images
* Set locations
* Set prices
* Set duration
* Set capacity
* Define availability
* Add requirements
* Accept bookings

---

# 23. Services — Minor

Basic stay-related services can also be offered.

Examples:

* Cleaning
* Local guide
* Airport pickup
* Chef
* Photography
* Equipment rental
* Other stay-related services

The Minor scope will keep these services focused on improving the accommodation experience rather than becoming a full-scale service marketplace.

---

# 24. Guest Dashboard

The Guest Dashboard will include:

```text
My Bookings
Wishlist
Reviews
Reports
Notifications
Profile
AI Assistant
```

---

# 25. Host Dashboard

The Host Dashboard will include:

```text
My Properties
Bookings
Calendar
Requirements
Verification
Reviews
Earnings
Notifications
```

---

# 26. Admin Dashboard

The Admin Dashboard will provide:

```text
Users
Hosts
Properties
Bookings
Verification Requests
Reports
Reviews
Statistics
```

Admin capabilities include:

* Reviewing verification requests
* Approving/rejecting verification
* Reviewing reports
* Managing users
* Managing properties
* Moderating content
* Viewing platform statistics

---

# 27. Notifications

Minor notification system:

* Booking confirmation
* Payment status
* Booking cancellation
* Verification status
* Review reminders
* Report status
* Important booking updates

Implementation can use in-app notifications with email notifications where practical.

---

# 28. Basic Analytics

Admin analytics will include:

* Total users
* Total hosts
* Total properties
* Total bookings
* Revenue
* Pending verifications
* Reports
* Active listings

Possible visualizations:

* Booking trends
* User growth
* Property category distribution
* Verification status
* Booking status

---

# 29. Engineering Scope — Minor

The Minor Project will follow a modular and scalable architecture.

### Backend

* Node.js
* Express.js
* TypeScript
* API Gateway
* Modular domain structure

### Database

* PostgreSQL
* Prisma

### Supporting Infrastructure

* Redis
* RabbitMQ
* Docker
* Docker Compose
* Object storage where required

### API

* REST APIs
* OpenAPI / Swagger

---

# 30. Testing

Testing will be part of the Minor development process.

### Backend

* Authentication testing
* API testing
* Booking validation
* Verification testing
* AI API testing

### Frontend

* Important component testing

### Integration

Critical flows:

```text
Search
  ↓
Property
  ↓
Booking
  ↓
Payment
  ↓
Review
```

will be tested.

---

# 31. Docker

The Minor environment will be containerized where practical.

Example:

```text
Frontend
Backend
PostgreSQL
Redis
RabbitMQ
```

Docker Compose will help reproduce the local development environment.

---

# 32. Scalability Demonstration — Minor

Scalability will be **demonstrated rather than operated at production scale**.

The goal is to show how Vistara can evolve beyond a single application instance.

Example:

```text
                 Load Balancer
                /      |      \
               ↓       ↓       ↓
            App 1    App 2    App 3
                \      |      /
                 \     |     /
                  ↓    ↓    ↓
                  Database
                     +
                    Redis
```

Multiple local application instances can be used to demonstrate the concept.

No expensive production infrastructure is required for this demonstration.

---

# 33. Event-Driven Demonstration

RabbitMQ can be used for asynchronous workflows.

Example:

```text
Booking Created
      ↓
    Event
      ↓
  RabbitMQ
   ↙   ↓   ↘
Email Notification
Analytics
Other Background Task
```

This demonstrates how Vistara can reduce coupling between components.

---

# 34. Deployment — Minor

The Minor Project will be deployed as a working application.

```text
GitHub
   ↓
Build
   ↓
Deployment
   ↓
Live Vistara
```

The focus is on having a functional, demonstrable product rather than expensive production infrastructure.

---

# 🟡 PART B — MAJOR PROJECT

The Major Project will extend the Minor foundation.

---

# 35. Advanced AI

Major AI scope:

* ML-based recommendation
* Advanced personalization
* Advanced ranking
* Semantic search
* Advanced NLP
* Behaviour-based recommendation
* Review anomaly detection
* Behaviour anomaly detection
* Photo/image authenticity analysis
* Advanced AI support
* AI check-in assistant

---

# 36. Advanced Trust & Risk

Major will expand the Minor verification foundation into an advanced intelligence system.

```text
Identity
Business
Property
Documents
Reviews
Reports
Behaviour
      ↓
Advanced Risk Engine
      ↓
Risk Signals
```

Possible capabilities:

* Advanced risk scoring
* Fraud detection
* Behavioural risk analysis
* Advanced verification automation
* Cross-signal analysis
* Advanced moderation

---

# 37. Money Radar — Major

The full Money Radar system will provide deeper price intelligence.

Possible capabilities:

* Total-cost intelligence
* Fee analysis
* Price comparison
* Price trends
* Price anomaly detection
* Cost insights
* Advanced price transparency

---

# 38. Regulatory & Compliance — Major

Major will introduce regulatory/compliance capabilities.

Possible areas:

* Regulatory lookup
* Property compliance
* Host compliance
* Compliance status
* Regulatory information
* Compliance-related workflows

---

# 39. Real-Time Communication — Major

Major will introduce advanced communication:

* Guest-host messaging
* WebSocket-based communication
* Booking-based chat
* Real-time notifications
* Advanced communication workflows

---

# 40. Travel Agency — Major

Travel agencies will become part of the broader Vistara ecosystem.

Possible functionality:

* Agency profile
* Agency verification
* Travel packages
* Multi-day trips
* Group tours
* Itineraries
* Transport + accommodation packages
* Agency dashboard

---

# 41. Broader Tourism Marketplace — Major

The Major Project can expand beyond accommodation and basic experiences into:

* Art Galleries
* Museums
* Amusement / Entertainment
* Attractions
* Events
* Tour Operators
* Travel Businesses
* Larger Activity Providers

The long-term marketplace becomes:

```text
Accommodation
      +
Experiences
      +
Services
      +
Travel Agencies
      +
Tourism Businesses
```

---

# 42. Advanced Scalability — Major

Minor will demonstrate scalability.

Major can implement deeper scalable architecture:

```text
Modular Backend
      ↓
Service Extraction
      ↓
Microservices
      ↓
Event Driven
      ↓
Containers
      ↓
Load Balancer
      ↓
Auto Scaling
```

Possible technologies:

* Kubernetes
* AWS
* Load balancing
* Auto scaling
* Service discovery
* RabbitMQ/Kafka
* Redis scaling
* OpenSearch
* CI/CD
* Infrastructure as Code
* Prometheus
* Grafana
* OpenTelemetry
* Centralized logging

These technologies are part of the engineering roadmap; paid infrastructure is not required merely to demonstrate the architecture.

---

# 43. Final Minor vs Major Scope

| Module                    |  Minor  |       Major       |
| ------------------------- | :-----: | :---------------: |
| Hotel                     |    ✅    |                   |
| Apartment                 |    ✅    |                   |
| Villa                     |    ✅    |                   |
| Homestay                  |    ✅    |                   |
| Hostel                    |    ✅    |                   |
| Resort                    |    ✅    |                   |
| Cottage                   |    ✅    |                   |
| Cabin                     |    ✅    |                   |
| Guest House               |    ✅    |                   |
| Farm Stay                 |    ✅    |                   |
| Beach House               |    ✅    |                   |
| Luxury Home               |    ✅    |                   |
| Search & Filters          |    ✅    |      Advanced     |
| Map                       |    ✅    |                   |
| Booking                   |    ✅    |      Advanced     |
| Payment                   |    ✅    |      Advanced     |
| Wishlist                  |    ✅    |                   |
| Reviews                   |    ✅    |    Advanced AI    |
| Host Requirements         |    ✅    |                   |
| Guest Confirmation        |    ✅    |                   |
| Requirement Snapshot      |    ✅    |                   |
| Identity Verification     |    ✅    |      Advanced     |
| Business Verification     |    ✅    |      Advanced     |
| Property Verification     |    ✅    |      Advanced     |
| Document Verification     |    ✅    |      Advanced     |
| Trust Indicators          |    ✅    |                   |
| Basic Reports             |    ✅    |      Advanced     |
| AI Assistant              |    ✅    |      Advanced     |
| Natural Language Search   |    ✅    |  Semantic Search  |
| Basic Recommendation      |    ✅    | ML Recommendation |
| Basic AI Support          |    ✅    |    Advanced AI    |
| Experiences               | ✅ Basic |      Advanced     |
| Services                  | ✅ Basic |      Advanced     |
| Notifications             |    ✅    |     Real-time     |
| Guest Dashboard           |    ✅    |                   |
| Host Dashboard            |    ✅    |                   |
| Admin Dashboard           |    ✅    |      Advanced     |
| Basic Price Transparency  |    ✅    |    Money Radar    |
| Docker                    |    ✅    |                   |
| Redis                     |    ✅    |  Advanced Scaling |
| RabbitMQ                  | ✅ Basic |      Advanced     |
| Scalability Demonstration |    ✅    |                   |
| Deployment                |    ✅    |  Production-scale |
| Money Radar               |         |         ✅         |
| Advanced Risk Engine      |         |         ✅         |
| Fraud Detection           |         |         ✅         |
| ML Recommendation         |         |         ✅         |
| Review Anomaly Detection  |         |         ✅         |
| Photo Authenticity        |         |         ✅         |
| Regulatory Service        |         |         ✅         |
| Real-Time Messaging       |         |         ✅         |
| Travel Agency             |         |         ✅         |
| Art Gallery               |         |         ✅         |
| Museum                    |         |         ✅         |
| Amusement / Entertainment |         |         ✅         |
| Attractions / Events      |         |         ✅         |
| Tour Operators            |         |         ✅         |
| Kubernetes                |         |         ✅         |
| AWS Architecture          |         |         ✅         |
| Auto Scaling              |         |         ✅         |
| Advanced Observability    |         |         ✅         |

---

# 44. Minor User Journey

The final Minor user journey is:

```text
REGISTER / LOGIN
       ↓
SEARCH / AI SEARCH
       ↓
FILTER / CATEGORY / MAP
       ↓
PROPERTY DETAILS
       ↓
TRUST & VERIFICATION
       ↓
HOST REQUIREMENTS
       ↓
GUEST CONFIRMATION
       ↓
AVAILABILITY
       ↓
BOOKING
       ↓
PAYMENT
       ↓
STAY
       ↓
REVIEW / MISMATCH REPORT
       ↓
TRUST SYSTEM
       ↓
ADMIN REVIEW
```

AI works alongside the journey:

```text
User Query
    ↓
AI Understanding
    ↓
Search
    ↓
Trust Signals
    ↓
Recommendation
```

---

# 45. Final Vistara Scope

## Minor

> **A complete, deployable, AI-enabled and trust-aware accommodation marketplace with multiple property categories, experiences, basic services, verification, host requirements, guest confirmation, booking, payment, reviews, AI-assisted search and recommendation, dashboards, notifications, Docker, and demonstrated scalability.**

## Major

> **An advanced Vistara ecosystem extending the Minor foundation with advanced AI, ML recommendations, risk intelligence, fraud detection, Money Radar, regulatory compliance, real-time communication, travel agencies, broader tourism businesses, and deeper scalable infrastructure.**

---

# 46. Scope Freeze Principle

After Day 8:

> **The scope is frozen.**

New ideas will not automatically enter the Minor Project.

New ideas will be evaluated against:

```text
Does it solve the core problem?
        ↓
Does it fit the 90-day timeline?
        ↓
Does it improve Vistara meaningfully?
        ↓
Minor / Major / Future
```

This prevents uncontrolled feature expansion while keeping Vistara ambitious.

---

# 47. Day 8 Final Decision

```text
                 VISTARA
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
       MINOR                MAJOR
          │                   │
   Working Product      Advanced Product
          │                   │
 Marketplace            Advanced AI
 AI                     Advanced Trust
 Verification           Risk Engine
 Trust                   Money Radar
 Experiences             Regulatory
 Services                Real-time
 Booking                 Travel Agency
 Payment                 Tourism
 Reviews                 Advanced Scaling
 Dashboards
 Notifications
 Docker
 Scalability Demo
 Deployment
```

### Final Product Philosophy

> **Minor builds Vistara. Major makes Vistara intelligent, trust-aware, transparent, connected, and scalable.**

**Day 8 Output:** `DAY-08-MVP-AND-SCOPE.md`

# Vistara — Day 12: Data, Dataset & API Strategy

> **Build the data foundation first. Then build intelligence on top of it.**

Day 12 defines how Vistara will **collect, store, consume, process, and eventually learn from data**.

The strategy connects:

```text
External APIs
      +
Public / Open Data
      +
Seed Data
      +
Vistara User Data
      ↓
Backend
      ↓
Prisma
      ↓
Neon PostgreSQL
      ↓
Structured Application Data
      ↓
ML / AI Data Pipeline
      ↓
Partner's ML Models
      ↓
AI Services
      ↓
Vistara Frontend
```

---

# 1. Day 12 Objective

The main objectives are:

* Identify all data required by Vistara
* Identify where each data type will come from
* Decide which APIs are required
* Decide which data will be stored in Neon PostgreSQL
* Define Prisma's role
* Define seed-data strategy
* Define public/open-data strategy
* Define first-party data collection
* Define ML dataset requirements
* Define API-to-database flow
* Define ML-to-backend integration
* Define data privacy and licensing considerations

---

# 2. Core Data Architecture

Vistara will use **Neon PostgreSQL as the primary application database**.

```text
                    VISTARA
                       │
                    Backend
                       │
                    Prisma
                       │
              Neon PostgreSQL
                       │
      ┌────────────────┼────────────────┐
      ↓                ↓                ↓
   Users          Properties         Bookings
      ↓                ↓                ↓
 Preferences       Reviews          Payments
      ↓                ↓                ↓
 User Events     Verification      Trust Signals
                       │
                       ↓
                 Structured Data
                       │
                       ↓
                  ML Pipeline
```

---

# 3. Data Source Strategy

Vistara will use four main data sources.

```text
                    DATA SOURCES
                         │
       ┌─────────────────┼─────────────────┐
       ↓                 ↓                 ↓
   FIRST-PARTY       EXTERNAL APIs      PUBLIC DATA
       │                 │                 │
       ↓                 ↓                 ↓
 Vistara Users       Live Data        Open Datasets
 Hosts               Services         Geographic Data
 System Events       AI / Maps        Tourism Data
                         │
                         ↓
                    SEED DATA
```

---

# 4. Source 1 — Vistara First-Party Data

This is the most important long-term data source.

The application itself will generate data through normal usage.

## User Data

```text
User
Profile
Preferences
Searches
Wishlist
Bookings
Reviews
Reports
```

## Host Data

```text
Host Profile
Properties
Amenities
Availability
Pricing
Requirements
Property Updates
```

## Behaviour Data

```text
Search
Property View
Wishlist
Booking
Cancellation
Review
AI Query
Filter Usage
```

This data can later support recommendation and personalization.

---

# 5. Source 2 — External APIs

External APIs will provide information that Vistara should not maintain manually.

Main categories:

```text
Maps / Location
Weather
Payments
AI / LLM
Geographic Information
Verification Services where available
Object Storage
```

---

# 6. API Strategy

We will not use an API simply because it exists.

Every API must be evaluated on:

```text
API
 ↓
Data Quality
 ↓
India Coverage
 ↓
Cost
 ↓
Rate Limits
 ↓
License / Terms
 ↓
Reliability
 ↓
Need in Minor?
 ↓
Final Decision
```

---

# 7. Maps & Location API

## Primary Options

### Option A — OpenStreetMap ecosystem

Useful for:

* Geographic data
* Map context
* Coordinates
* Geocoding through appropriate services

The public Nominatim service has strict usage rules: maximum 1 request/second, a valid identifying User-Agent/Referer, attribution, caching where appropriate, and it explicitly does not support client-side autocomplete. It also discourages heavy/bulk use.

Therefore:

> **We should not design Vistara around heavy direct use of the public Nominatim server.**

For a small prototype, controlled use may be possible if its policy is followed. For larger usage, we should use a suitable provider or operate our own infrastructure.

---

### Option B — Google Maps Platform

Google Maps Platform provides:

* Maps
* Geocoding
* Places
* Routes
* Location services

For India-based eligible customers, Google currently provides India-specific pricing and recurring free usage thresholds for many Core Services. Current documentation lists, for example, 70,000 monthly free billable events for several India Essentials SKUs, with usage-based pricing beyond the threshold.

Google's newer Places API is the preferred direction; its documentation notes that legacy Places/Directions/Distance Matrix services are transitioning to newer versions.

### Vistara Decision

For Minor:

```text
Map UI
+
Coordinates
+
Basic location search
```

Use a suitable map/location provider depending on final cost and usage.

**Do not make Google Maps mandatory until API usage/cost is confirmed for the actual implementation.**

---

# 8. Weather API

Weather is not the core Vistara marketplace feature, so it remains optional/supporting.

## Open-Meteo

Open-Meteo provides forecast APIs using latitude/longitude and supports forecast data for multiple days.

Possible use:

```text
Property / Destination
        ↓
Latitude + Longitude
        ↓
Weather API
        ↓
Destination Weather
```

Example UI:

```text
GOA

28°C
Sunny

Best for:
Beach activities
Outdoor experiences
```

### Scope

```text
Minor → Optional supporting feature
Major → Can be expanded into travel intelligence
```

---

# 9. Payment API

For India-focused development, **Razorpay** is a practical payment integration candidate.

Razorpay provides REST APIs for payments and orders, and its documentation supports test-mode integration before live payments.

For checkout, the application should create an order and associate the payment with the booking. Razorpay's documentation specifically notes that an `order_id` should be created before initiating payment for proper capture flow.

Architecture:

```text
Guest
 ↓
Booking
 ↓
Backend
 ↓
Razorpay Order
 ↓
Checkout
 ↓
Payment
 ↓
Webhook / Verification
 ↓
Payment Status
 ↓
Booking Status
```

### Important

We will use:

```text
Test Mode
```

during development.

Real-money payments are not required for the Minor demo.

---

# 10. AI / LLM API

The AI layer will support:

```text
AI Travel Assistant
Natural Language Search
Query Understanding
Basic Recommendations
AI-assisted Support
```

Architecture:

```text
User
 ↓
Frontend
 ↓
Backend
 ↓
AI Provider
 ↓
Structured Response
 ↓
Backend Validation
 ↓
Search / Recommendation
 ↓
Frontend
```

The AI provider should be configurable through environment variables.

```text
AI_PROVIDER
AI_API_KEY
AI_MODEL
```

This prevents the application from being tightly coupled to one provider.

---

# 11. AI Data Rule

AI output should **not directly control critical operations**.

For example:

```text
AI
 ↓
"Property available"
 ↓
❌ Do not trust blindly
```

Instead:

```text
AI Suggestion
      ↓
Backend
      ↓
Database Validation
      ↓
Business Rules
      ↓
Final Result
```

This is especially important for:

* Availability
* Price
* Payment
* Verification
* Booking

---

# 12. Verification APIs

Verification is a sensitive area.

Possible future integrations:

```text
Identity Verification
Business Verification
Document Verification
Certificate Verification
```

But we will **not randomly connect to an unverified third-party API**.

For each provider we must check:

```text
Legal availability
API access
India support
Pricing
Data handling
Privacy
Terms
Accuracy
```

### Minor

We can demonstrate the verification workflow using:

```text
User Input
+
Document Metadata
+
Admin Review
+
Verification Status
```

without requiring expensive third-party verification infrastructure.

### Major

Authorized verification providers can be integrated later.

---

# 13. Image Storage API

Property images should not be stored directly inside PostgreSQL as large binary data.

Architecture:

```text
Host
 ↓
Image Upload
 ↓
Object Storage
 ↓
Image URL / Key
 ↓
PostgreSQL
```

Database stores:

```text
propertyId
imageUrl
storageKey
metadata
```

Possible storage:

```text
S3-compatible storage
Cloud object storage
```

---

# 14. External API Summary

| Data            | API / Source                              | Minor    |
| --------------- | ----------------------------------------- | -------- |
| Maps            | Google Maps / suitable OSM-based provider | ✓        |
| Geocoding       | Suitable provider                         | ✓        |
| Weather         | Open-Meteo                                | Optional |
| Payment         | Razorpay                                  | ✓        |
| AI              | Configurable LLM provider                 | ✓        |
| Verification    | Authorized provider / internal workflow   | ✓        |
| Images          | Object Storage                            | ✓        |
| Advanced Search | OpenSearch later                          | Major    |

---

# 15. Data We Will NOT Simply Copy

Vistara should not build its database by blindly copying another booking platform's:

* Properties
* Reviews
* Host profiles
* Photos
* Prices
* User data

Instead:

```text
Vistara Host
      ↓
Creates Property
      ↓
Vistara Database
```

For public/open data:

```text
Public Dataset
      ↓
Check License
      ↓
Check Allowed Usage
      ↓
Transform
      ↓
Use With Attribution / Requirements
```

---

# 16. Seed Data Strategy

For initial development we need data before real users exist.

Therefore we will create controlled seed data.

Example:

```text
100–500 Properties
20–50 Destinations
Multiple Property Categories
Amenities
Sample Availability
Sample Prices
Sample Hosts
Sample Reviews
Sample Experiences
Sample Services
```

This data is clearly treated as:

> **Development / Demo Data**

It must not be represented as real user-generated reviews or real verified properties.

---

# 17. Initial Seed Destinations

We can initially focus on selected Indian destinations.

Example:

```text
Goa
Jaipur
Udaipur
Manali
Rishikesh
Mumbai
Delhi
Bengaluru
Kerala
Varanasi
```

The list can change based on project scope.

---

# 18. Property Seed Data

Each property should contain realistic structured attributes.

```text
Property
├── Name
├── Category
├── Location
├── Coordinates
├── Description
├── Price
├── Capacity
├── Amenities
├── Images
├── Availability
├── House Rules
└── Requirements
```

---

# 19. Prisma + Neon PostgreSQL

The main application data store:

```text
Neon PostgreSQL
        ↑
      Prisma
        ↑
    Backend
```

Prisma handles:

* Schema
* Queries
* Relations
* Migrations
* Type-safe database access

Neon provides:

* PostgreSQL database
* Cloud-hosted development database
* Connection to backend
* Persistent application data

---

# 20. Core Database Domains

```text
DATABASE
│
├── USER
│
├── GUEST_PROFILE
│
├── HOST_PROFILE
│
├── PROPERTY
│
├── PROPERTY_IMAGE
│
├── AMENITY
│
├── AVAILABILITY
│
├── BOOKING
│
├── PAYMENT
│
├── REVIEW
│
├── WISHLIST
│
├── VERIFICATION
│
├── REQUIREMENT
│
├── REQUIREMENT_SNAPSHOT
│
├── MISMATCH_REPORT
│
├── TRUST_SIGNAL
│
├── AI_CONVERSATION
│
├── AI_MESSAGE
│
├── USER_EVENT
│
├── EXPERIENCE
│
└── SERVICE
```

---

# 21. User Data

```text
USER
├── id
├── name
├── email
├── passwordHash
├── role
├── createdAt
└── updatedAt
```

Sensitive credentials must never be used as ML features.

---

# 22. Guest Preference Data

Potential preference information:

```text
GUEST_PROFILE
├── preferredLocation
├── preferredPropertyType
├── budgetRange
├── preferredAmenities
├── travelStyle
└── other non-sensitive preferences
```

These fields should only be collected where they support actual functionality.

---

# 23. Host Data

```text
HOST_PROFILE
├── id
├── userId
├── bio
├── responseRate
├── responseTime
└── verificationStatus
```

---

# 24. Property Data

```text
PROPERTY
├── id
├── hostId
├── title
├── description
├── category
├── location
├── latitude
├── longitude
├── pricePerNight
├── guestCapacity
├── verificationStatus
├── createdAt
└── updatedAt
```

---

# 25. Property Supporting Data

```text
PROPERTY
│
├── PROPERTY_IMAGE
├── PROPERTY_AMENITY
├── AVAILABILITY
├── PROPERTY_REQUIREMENT
├── PROPERTY_VERIFICATION
└── TRUST_SIGNAL
```

This keeps the database normalized and easier to maintain.

---

# 26. Booking Data

```text
BOOKING
├── id
├── guestId
├── propertyId
├── checkIn
├── checkOut
├── guestCount
├── basePrice
├── cleaningFee
├── taxes
├── totalPrice
├── status
└── createdAt
```

---

# 27. Requirement Snapshot

At booking time:

```text
PROPERTY REQUIREMENTS
        ↓
Guest sees them
        ↓
Guest confirms
        ↓
Snapshot stored
        ↓
BOOKING
```

Example:

```text
REQUIREMENT_SNAPSHOT

bookingId
maxGuests
idRequired
petPolicy
smokingPolicy
checkInRule
checkOutRule
houseRules
confirmedAt
```

This allows later comparison between:

```text
Requirement shown at booking
              VS
Requirement / experience later reported
```

---

# 28. Review Data

```text
REVIEW
├── id
├── bookingId
├── propertyId
├── guestId
├── overallRating
├── cleanlinessRating
├── locationRating
├── accuracyRating
├── communicationRating
├── valueRating
├── reviewText
└── createdAt
```

This structure supports both:

```text
Traditional Rating
+
Structured Review Analysis
```

---

# 29. Mismatch Data

```text
MISMATCH_REPORT
├── id
├── bookingId
├── propertyId
├── category
├── description
├── evidence
├── status
└── createdAt
```

Categories:

```text
PROPERTY_DESCRIPTION
AMENITY
ROOM_CONDITION
LOCATION
HOUSE_RULE
HOST_REQUIREMENT
OTHER
```

---

# 30. Verification Data

```text
VERIFICATION
├── id
├── targetId
├── targetType
├── verificationType
├── status
├── submittedAt
├── reviewedAt
└── result
```

Types:

```text
IDENTITY
BUSINESS
PROPERTY
CERTIFICATE
DOCUMENT
```

---

# 31. Trust Data

Trust signals combine multiple sources.

```text
VERIFICATION
       +
REVIEWS
       +
MISMATCH REPORTS
       +
PROPERTY INFORMATION
       +
BEHAVIOUR SIGNALS
       ↓
TRUST SIGNALS
```

Example:

```text
TRUST_SIGNAL
├── propertyId
├── signalType
├── source
├── status
├── confidence
└── createdAt
```

Advanced risk scoring belongs to Major.

---

# 32. User Behaviour Data

This is particularly important for future ML.

```text
USER_EVENT
├── id
├── userId
├── eventType
├── propertyId
├── searchQuery
├── metadata
└── timestamp
```

Possible events:

```text
SEARCH
VIEW_PROPERTY
CLICK_PROPERTY
ADD_WISHLIST
REMOVE_WISHLIST
START_BOOKING
COMPLETE_BOOKING
CANCEL_BOOKING
VIEW_REVIEW
SUBMIT_REVIEW
AI_QUERY
FILTER_USED
```

---

# 33. AI Conversation Data

```text
AI_CONVERSATION
├── id
├── userId
├── createdAt
└── context

AI_MESSAGE
├── id
├── conversationId
├── role
├── content
└── createdAt
```

Example:

```text
User:
"Find a peaceful villa in Goa under ₹8,000."

AI:
"Here are matching properties..."
```

Privacy and retention rules should be applied before using conversation data for ML.

---

# 34. Price Data

Minor:

```text
Base Price
+
Cleaning Fee
+
Taxes
=
Estimated Total
```

Major can introduce:

```text
PRICE_HISTORY
├── propertyId
├── price
├── date
├── source
└── context
```

This can support Money Radar.

---

# 35. Data → ML Pipeline

This is the connection between your work and your partner's work.

```text
                VISTARA APP
                     │
                     ↓
              Neon PostgreSQL
                     │
                     ↓
             Structured Data
                     │
                     ↓
             Data Extraction
                     │
                     ↓
            Cleaning / Processing
                     │
                     ↓
               ML Dataset
                     │
                     ↓
             Partner's ML Work
                     │
                     ↓
              Model / Output
                     │
                     ↓
               Backend API
                     │
                     ↓
                 Frontend
```

---

# 36. ML Dataset Sources

Your partner can use two categories of datasets.

## A. Public / Research Datasets

Used for:

```text
Model experimentation
Benchmarking
Initial training
Feature exploration
```

Possible categories:

```text
Recommendation datasets
Review sentiment datasets
Property price datasets
Geographic datasets
Fraud / anomaly datasets
```

Every dataset must be checked for:

```text
License
Allowed usage
Attribution
Commercial restrictions
Data quality
```

---

## B. Vistara First-Party Dataset

Eventually the strongest project-specific dataset will come from Vistara itself.

```text
Users
 ↓
Interactions
 ↓
Bookings
 ↓
Reviews
 ↓
Feedback
 ↓
Dataset
```

This can support:

```text
Recommendation
Personalization
Review Classification
Trust Signals
Behaviour Analysis
```

---

# 37. What Goes Into Neon?

### YES — Application Data

```text
Users
Hosts
Properties
Amenities
Availability
Bookings
Payments Metadata
Reviews
Wishlists
Requirements
Verification Status
Trust Signals
Experiences
Services
AI Conversations where appropriate
User Events
```

### NO — Raw Secrets

Do not store:

```text
Passwords in plain text
API Keys
Payment secrets
LLM API Keys
Private infrastructure credentials
```

---

# 38. What Goes Into the ML Dataset?

Only appropriate, processed data.

Example:

```text
USER_ID
PROPERTY_ID
EVENT_TYPE
PROPERTY_CATEGORY
LOCATION
PRICE_RANGE
AMENITY_SIGNAL
RATING
BOOKING_SIGNAL
TIMESTAMP
```

Sensitive information should be removed or transformed when not required.

---

# 39. Data Processing Pipeline

```text
Raw Application Data
        ↓
Validation
        ↓
Cleaning
        ↓
Deduplication
        ↓
Normalization
        ↓
Feature Engineering
        ↓
Train / Validation / Test
        ↓
ML Model
```

---

# 40. API → Database Flow

External API data should normally pass through the backend.

```text
Frontend
   ↓
Backend
   ↓
External API
   ↓
Validation / Transformation
   ↓
Database if persistence is needed
   ↓
Frontend
```

Do not expose secret API keys directly in the browser.

---

# 41. Example — Location

```text
User enters:

"Goa"
     ↓
Frontend
     ↓
Backend
     ↓
Geocoding / Places API
     ↓
Coordinates
     ↓
PostgreSQL
     ↓
Search
```

---

# 42. Example — Weather

```text
Property Coordinates
        ↓
Weather API
        ↓
Current / Forecast Data
        ↓
Vistara Backend
        ↓
Destination UI
```

Weather can remain a live API response rather than being permanently stored unless there is a product reason to cache it.

---

# 43. Example — Payment

```text
Guest
 ↓
Booking
 ↓
Backend
 ↓
Razorpay Order
 ↓
Checkout
 ↓
Payment
 ↓
Webhook
 ↓
Backend Verification
 ↓
Payment Record
 ↓
Booking Confirmed
```

Razorpay recommends webhooks for receiving event notifications, and its documentation provides test-mode keys for development.

---

# 44. Example — AI Search

```text
User:
"Quiet villa near beach under ₹8k"

        ↓

AI API

        ↓

Structured Intent

destination = Goa
propertyType = Villa
budget = 8000
preference = Quiet
location = Beach

        ↓

Backend Validation

        ↓

PostgreSQL Search

        ↓

Property Results
```

---

# 45. Example — Recommendation

```text
User Events
     +
Preferences
     +
Property Data
     +
Reviews
     +
Bookings
     ↓
Recommendation Logic
     ↓
Ranked Properties
     ↓
Frontend
```

Minor can start with:

```text
Rule-based
+
Content-based
+
Basic preference matching
```

Major can move toward:

```text
ML Ranking
+
Collaborative Filtering
+
Embeddings
+
Personalization
+
Behaviour Modeling
```

---

# 46. API Cost Strategy

Vistara is a student project, so we should avoid unnecessary paid infrastructure.

### Development Principle

```text
Free / Open
      ↓
Low-cost
      ↓
Pay-as-you-grow
      ↓
Major Production Infrastructure
```

Examples:

```text
Neon
→ PostgreSQL development

Open-Meteo
→ Weather

Open/public geographic data
→ Location research where appropriate

Razorpay Test Mode
→ Payment development

AI API
→ Controlled development usage
```

Google Maps Platform is viable but usage-based; current India pricing includes free monthly thresholds for several services and paid usage beyond them, so we should monitor usage rather than assume it is unlimited/free.

---

# 47. Data Privacy

The project should follow a data-minimization principle.

```text
Need Data?
    ↓
Yes → Collect
    ↓
Protect
    ↓
Use for stated purpose
```

Avoid collecting sensitive information merely because it could someday be useful for ML.

Particularly sensitive information such as identity documents and payment credentials should not be treated as ordinary ML training data.

---

# 48. Data Licensing

For every external dataset/API:

```text
Source
License
Allowed Usage
Attribution
Commercial Restrictions
API Limits
Retention Rules
```

must be documented.

For example, OpenStreetMap data is under ODbL and its public Nominatim service has additional operational restrictions.

---

# 49. Minor Data Scope

```text
✓ Seed Property Data
✓ User Data
✓ Host Data
✓ Property Data
✓ Search Data
✓ Wishlist Data
✓ Booking Data
✓ Review Data
✓ Verification Status
✓ Requirement Data
✓ Mismatch Data
✓ Trust Signals
✓ AI Queries
✓ Basic Behaviour Events
✓ Basic Price Data
✓ Location / Map Data
✓ Payment Test Data
```

---

# 50. Major Data Scope

```text
→ Large-scale Behaviour Data
→ Advanced Recommendation Dataset
→ Advanced Price History
→ Risk / Fraud Signals
→ Image Dataset
→ Advanced Review Dataset
→ Real-time Behaviour Streams
→ Advanced Semantic Search Data
→ Regulatory Data
→ Tourism Marketplace Data
```

---

# 51. Final API Architecture

```text
                         VISTARA
                            │
                         Backend
                            │
          ┌─────────────────┼──────────────────┐
          ↓                 ↓                  ↓
      PostgreSQL         External APIs        AI
       / Prisma               │                │
          │                   │                │
          │          ┌────────┼────────┐       │
          │          ↓        ↓        ↓       │
          │        Maps    Weather  Payment   LLM
          │
          ↓
     Application Data
          │
          ↓
      ML Pipeline
          │
          ↓
    Partner's Models
          │
          ↓
      AI Services
```

---

# 52. Final Data Architecture

```text
                         USER
                          │
                          ↓
                    VISTARA APP
                          │
             ┌────────────┼────────────┐
             ↓            ↓            ↓
        User Events    Bookings     Reviews
             │            │            │
             └────────────┼────────────┘
                          ↓
                     BACKEND API
                          │
             ┌────────────┼────────────┐
             ↓            ↓            ↓
          Prisma       External       AI
             │           APIs          │
             ↓            │            │
       Neon PostgreSQL    │            │
             │            │            │
             └────────────┼────────────┘
                          ↓
                   Structured Data
                          ↓
                    ML Data Pipeline
                          ↓
                    ML / AI Models
                          ↓
                     Backend APIs
                          ↓
                       Frontend
```

---

# 53. Day 12 Deliverables

At the end of Day 12, the team should have:

```text
[✓] Primary database selected
[✓] Neon PostgreSQL selected
[✓] Prisma selected
[✓] Core entities identified
[✓] Data sources identified
[✓] External API categories identified
[✓] Maps strategy
[✓] Weather strategy
[✓] Payment API strategy
[✓] AI API strategy
[✓] Verification strategy
[✓] Image storage strategy
[✓] Seed-data strategy
[✓] Public-data strategy
[✓] First-party data strategy
[✓] ML dataset strategy
[✓] User behaviour events
[✓] Data privacy principles
[✓] Data licensing principles
[✓] API → Backend architecture
[✓] Backend → Database architecture
[✓] Database → ML pipeline
[✓] Minor vs Major data scope
```

---

# 54. Final Day 12 Decision

The final Vistara data strategy is:

```text
                 DATA
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
   OUR DATA     API DATA    PUBLIC DATA
       │           │           │
       ↓           ↓           ↓
    Users       Maps        Geography
    Hosts       Weather     Open Data
    Properties  Payment     ML Datasets
    Bookings    AI
    Reviews
       │
       └───────────┬───────────┘
                   ↓
             BACKEND
                   ↓
              PRISMA ORM
                   ↓
          NEON POSTGRESQL
                   ↓
          STRUCTURED DATA
                   ↓
             ML PIPELINE
                   ↓
          PARTNER'S MODELS
                   ↓
              AI OUTPUT
                   ↓
              VISTARA UI
```

---

# Final Statement

> **Vistara will not depend on one external dataset or one API.**

The platform will combine:

**First-party application data + controlled seed data + authorized external APIs + appropriate public/open datasets.**

The actual product database remains:

> **Neon PostgreSQL + Prisma**

while ML data is created through a separate processing pipeline from appropriate structured data.

This gives Vistara a clean progression:

```text
Day 11
ML Research
      ↓
Day 12
Data + API + Database Strategy
      ↓
Day 13
Research Conclusion
      ↓
Day 14
Phase 1 Review
```

**Day 12 — Data, Dataset & API Strategy Complete.**

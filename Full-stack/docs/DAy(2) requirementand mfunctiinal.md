# Vistara — Day 9: Functional Requirements & Product Experience

> **Don't just find a stay. Know what you're booking.**

Day 9 defines the **functional behaviour, user-facing experience, system requirements, AI interaction, review system, trust flow, and product design direction** of Vistara.

The requirements are based on the frozen Day 8 MVP scope. No unrelated features are introduced.

---

# 1. Day 9 Objective

The objective of Day 9 is to define:

* What Vistara must do
* How users interact with the platform
* What the backend must support
* What information the AI layer receives and returns
* How reviews work
* How trust and verification interact with bookings
* How requirements are communicated
* How the UI presents information
* How the complete user journey works

The result is a **testable Functional Requirements Specification** for development.

---

# 2. Functional Requirement Format

Each requirement follows a common structure:

```text
Requirement ID
Actor
Requirement
Input
System Behaviour
Output
Acceptance Condition
```

Example:

```text
FR-BOOK-01

Actor:
Guest

Requirement:
Guest must be able to create a booking for an available property.

Input:
Property
Dates
Number of guests
Requirement confirmation

System Behaviour:
System validates availability and booking requirements.

Output:
Booking record

Acceptance:
Booking is created only when the property is available
and required confirmations are completed.
```

---

# 3. User Roles

Vistara supports three primary roles.

```text
USER
 │
 ├── GUEST
 │
 ├── HOST
 │
 └── ADMIN
```

### Guest

Can:

* Search properties
* Use AI search
* View property details
* View verification
* View reviews
* View requirements
* Confirm requirements
* Book
* Pay
* Cancel according to policy
* Add wishlist
* Review completed stays
* Report mismatches
* Use experiences/services

### Host

Can:

* Create host profile
* Add properties
* Manage property information
* Upload property images
* Define amenities
* Define availability
* Define pricing
* Define requirements
* View bookings
* Manage booking-related information
* View reviews
* Respond to reviews
* Submit verification information

### Admin

Can:

* Manage users
* Manage properties
* Review verification
* Review reports
* Review suspicious cases
* Manage trust signals
* Moderate reviews
* View system analytics

---

# 4. Authentication Requirements

## FR-AUTH-01 — Registration

Users must be able to create an account.

**Input:**

* Name
* Email
* Password
* Role where applicable

**Output:**

* User account
* Authentication session

**Acceptance:**

Account is created only when required information is valid.

---

## FR-AUTH-02 — Login

Users must be able to securely log in.

```text
Email + Password
       ↓
Authentication
       ↓
Session
       ↓
Role-based Dashboard
```

---

## FR-AUTH-03 — Role-Based Access

The system must restrict functionality based on user role.

```text
Guest → Guest Features
Host  → Host Features
Admin → Administrative Features
```

---

# 5. User & Profile Requirements

## FR-USER-01 — Guest Profile

Guest must be able to:

* View profile
* Edit profile
* Manage preferences
* View bookings
* View wishlist
* View reviews

---

## FR-USER-02 — Host Profile

Host profile may contain:

* Name
* Profile image
* Hosting information
* Verification status
* Response information
* Business information where applicable

---

# 6. Property Management Requirements

## FR-PROP-01 — Create Property

Host must be able to create a property listing.

Property information includes:

* Name
* Description
* Property type
* Location
* Price
* Guest capacity
* Amenities
* Images
* Availability
* House rules
* Host requirements

---

## FR-PROP-02 — Property Categories

Vistara Minor supports:

```text
Hotel
Apartment
Villa
Homestay
Hostel
Resort
Cottage
Cabin
Guest House
Farm Stay
Beach House
Luxury Home
```

---

## FR-PROP-03 — Update Property

Host must be able to modify property information.

---

## FR-PROP-04 — Property Images

Host must be able to add and manage property images.

The system stores:

* Image
* Property relationship
* Metadata where applicable

---

## FR-PROP-05 — Property Availability

The system must maintain property availability for booking.

---

# 7. Search & Discovery Requirements

## FR-SEARCH-01 — Basic Search

Users must be able to search using:

* Location
* Dates
* Guests

---

## FR-SEARCH-02 — Filters

Users must be able to filter by:

* Price
* Property type
* Amenities
* Guest capacity
* Rating
* Availability
* Relevant property characteristics

---

## FR-SEARCH-03 — Sorting

Users should be able to sort results using supported options such as:

* Price
* Rating
* Relevance

---

## FR-SEARCH-04 — Natural Language Search

Users can describe their requirements naturally.

Example:

> "Find me a peaceful villa near the beach for four people with a pool."

The system extracts relevant search parameters.

```text
Destination → Goa
Guests → 4
Property → Villa
Location preference → Beach
Amenity → Pool
Preference → Peaceful
```

---

# 8. Map Requirements

## FR-MAP-01 — Interactive Map

The system should display properties on an interactive map.

---

## FR-MAP-02 — Map & List Synchronization

Selecting a property from the map should identify the corresponding property result.

Selecting a property result should identify its map location.

---

# 9. Property Detail Requirements

## FR-PROP-06 — Property Detail Page

Users must be able to view:

* Property gallery
* Property name
* Property type
* Location
* Description
* Amenities
* Pricing
* Availability
* Host
* Verification
* Requirements
* Reviews
* Nearby experiences
* Services

---

# 10. Property Experience Design

Vistara will not treat the property page as a simple booking page.

The information hierarchy is:

```text
Hero
 ↓
Property Story
 ↓
Location
 ↓
Amenities
 ↓
Host
 ↓
Verification
 ↓
Requirements
 ↓
Reviews
 ↓
Nearby Experiences
 ↓
Services
 ↓
Booking
```

This creates a more detailed, destination-oriented experience.

---

# 11. Review System

Reviews are part of Vistara's trust system.

## FR-REVIEW-01 — Create Review

A guest can review a completed stay.

Review information can include:

* Overall rating
* Cleanliness
* Location
* Accuracy
* Communication
* Value
* Written experience
* Guest photographs

---

## FR-REVIEW-02 — Verified Stay

A review associated with a completed booking may display:

```text
✓ Verified Stay
```

This helps users understand the source of the experience.

---

## FR-REVIEW-03 — Review Summary

Property pages should present structured review information.

Example:

```text
4.8 ★

Cleanliness       4.9
Location          4.8
Accuracy          4.7
Communication     4.9
Value             4.6
```

---

## FR-REVIEW-04 — Host Response

Hosts should be able to respond to reviews where supported by the moderation rules.

---

# 12. Post-Stay Mismatch Reporting

## FR-REVIEW-05 — Mismatch Report

After a stay, guests can report differences between the listing and actual experience.

Examples:

* Property description differed
* Amenity unavailable
* Room condition differed
* House rule differed
* Location information was misleading
* Requirement differed from what was displayed

Flow:

```text
LISTING CLAIM
      ↓
ACTUAL EXPERIENCE
      ↓
MATCH / MISMATCH
      ↓
REVIEW / REPORT
```

---

# 13. Trust & Verification Requirements

## FR-VERIFY-01 — Identity Verification

The system must support identity verification status for applicable users.

---

## FR-VERIFY-02 — Business Verification

Where applicable, host/business information can be verified.

---

## FR-VERIFY-03 — Property Verification

Property verification status must be represented.

---

## FR-VERIFY-04 — Certificate / Document Verification

The system supports certificate/document verification workflows within the defined project scope.

---

## FR-VERIFY-05 — Verification Status

Supported statuses:

```text
PENDING
VALIDATING
RISK ANALYSIS
VERIFIED
REJECTED
REVIEW REQUIRED
```

Important:

> **Review Required / Suspicious does not automatically mean fraud.**

It indicates that additional review may be necessary.

---

# 14. Trust Indicators

Property and host pages should clearly communicate trust signals.

Example:

```text
YOUR TRUST CHECK

✓ Host Identity Verified
✓ Property Verified
✓ Business Verified
✓ Documents Checked
```

The UI should make verification visible without overwhelming the user.

---

# 15. Host Requirements

## FR-REQ-01 — Define Requirements

Host can define applicable requirements.

Examples:

```text
Maximum guests
ID requirement
Age requirement where applicable
Pet policy
Smoking policy
Check-in rules
Check-out rules
House rules
Other property-specific requirements
```

---

## FR-REQ-02 — Display Requirements

Requirements must be visible before booking.

---

## FR-REQ-03 — Guest Confirmation

Guest must confirm that they have reviewed applicable requirements.

```text
☑ I have read and agree to the requirements.
```

---

## FR-REQ-04 — Requirement Snapshot

The requirements presented at booking time must be associated with the booking.

```text
BOOKING
│
├── Property
├── Guest
├── Dates
├── Price
│
└── Requirement Snapshot
      ├── Guest Limit
      ├── ID Requirement
      ├── House Rules
      ├── Check-in Rules
      └── Other Requirements
```

This creates a historical reference if requirements change later.

---

# 16. Trust Feedback Loop

Vistara connects verification, booking and reviews.

```text
HOST CLAIM
     ↓
VERIFICATION
     ↓
PROPERTY LISTED
     ↓
GUEST BOOKS
     ↓
STAY
     ↓
GUEST EXPERIENCE
     ↓
MATCH / MISMATCH
     ↓
REVIEW / REPORT
     ↓
TRUST SIGNAL
     ↓
ADMIN REVIEW
```

This is a fundamental Vistara product mechanism.

---

# 17. AI Functional Requirements

AI is included in the Minor scope.

## FR-AI-01 — AI Travel Assistant

Users can interact with an AI travel assistant.

The assistant can help with:

* Destination discovery
* Property discovery
* Search refinement
* Preference interpretation
* Basic travel assistance

---

## FR-AI-02 — Query Understanding

AI should convert natural-language requests into structured parameters.

```text
Natural Language
       ↓
Intent Extraction
       ↓
Structured Parameters
       ↓
Search
       ↓
Property Results
```

---

## FR-AI-03 — Basic Recommendation

The system should provide basic recommendation based on available:

* User preferences
* Property attributes
* Search context
* Reviews
* Location
* Price

---

## FR-AI-04 — Trust-Aware Discovery

Where supported, recommendation logic can consider trust and verification signals.

Conceptually:

```text
USER PREFERENCES
       +
PROPERTY DATA
       +
REVIEWS
       +
VERIFICATION
       +
TRUST SIGNALS
       +
PRICE
       +
LOCATION
       ↓
TRUST-AWARE DISCOVERY
```

Advanced ML ranking and personalization remain part of the Major phase.

---

# 18. Price Transparency

## FR-PRICE-01 — Price Breakdown

The system should communicate major price components.

Example:

```text
Stay                 ₹5,000
Cleaning             ₹800
Taxes                ₹900
────────────────────────────
Estimated Total      ₹6,700
```

The full Money Radar intelligence belongs to the Major phase.

---

# 19. Booking Requirements

## FR-BOOK-01 — Availability Check

System must verify property availability before creating a booking.

---

## FR-BOOK-02 — Booking Creation

Guest can create a booking after:

```text
Availability Check
        ↓
Requirement Review
        ↓
Requirement Confirmation
        ↓
Price Review
        ↓
Payment
```

---

## FR-BOOK-03 — Booking Status

System should maintain booking status.

Example:

```text
PENDING
CONFIRMED
CANCELLED
COMPLETED
```

---

## FR-BOOK-04 — Booking History

Guest should be able to view past and upcoming bookings.

---

# 20. Payment Requirements

## FR-PAY-01 — Payment Initiation

Guest can initiate payment for a valid booking.

---

## FR-PAY-02 — Payment Status

System must maintain payment status.

```text
PENDING
SUCCESS
FAILED
REFUNDED
```

---

## FR-PAY-03 — Booking-Payment Relationship

Payment information must be associated with the relevant booking.

---

# 21. Wishlist Requirements

## FR-WISH-01

Guest can add a property to wishlist.

## FR-WISH-02

Guest can remove a property from wishlist.

## FR-WISH-03

Guest can view saved properties.

---

# 22. Experiences Requirements

Minor supports basic travel experiences.

```text
Local Food
City Tour
Photography Walk
Adventure Activity
Cultural Experience
Workshop
Nature Experience
Local Guide
```

## FR-EXP-01

Users can discover experiences associated with destinations.

## FR-EXP-02

Experience details can include:

* Name
* Description
* Location
* Price where applicable
* Provider
* Images
* Basic availability

---

# 23. Services Requirements

Minor supports stay-related services.

```text
Cleaning
Airport Pickup
Chef
Photography
Equipment Rental
Local Guide
Other Stay Services
```

## FR-SVC-01

Users can discover available services.

## FR-SVC-02

Service information should include relevant provider and service details.

---

# 24. Notification Requirements

## FR-NOTIF-01

System should notify users about important events.

Examples:

* Booking confirmation
* Payment status
* Cancellation
* Verification updates
* Important booking changes

Notifications may be implemented through:

```text
In-App
Email
```

where practical.

---

# 25. Dashboard Requirements

## FR-DASH-01 — Guest Dashboard

```text
My Trips
Upcoming
Past Trips
Wishlist
Reviews
Profile
AI Travel Assistant
```

---

## FR-DASH-02 — Host Dashboard

```text
Properties
Bookings
Calendar
Reviews
Verification
Requirements
Earnings
Guest Reports
```

---

## FR-DASH-03 — Admin Dashboard

```text
Users
Properties
Bookings
Verification
Reports
Trust Signals
Review Required Cases
Reviews
Analytics
```

---

# 26. Admin Requirements

## FR-ADMIN-01

Admin can manage users.

## FR-ADMIN-02

Admin can review properties.

## FR-ADMIN-03

Admin can review verification cases.

## FR-ADMIN-04

Admin can review reports and mismatch cases.

## FR-ADMIN-05

Admin can moderate relevant content.

---

# 27. Product Design Requirements

The functional system must be supported by a consistent product experience.

Vistara's visual direction combines:

```text
Moctale-inspired
Review Depth
       +
Soothey-inspired
Warm / Calm Visual Language
       +
Abu Dhabi-inspired
Destination Storytelling
       +
Vistara
Trust + AI + Verification
```

These are **design references, not direct copies**.

---

# 28. Visual Language

The interface should feel:

```text
Warm
   ↓
Calm
   ↓
Premium
   ↓
Trustworthy
   ↓
Travel-oriented
```

Avoid a generic marketplace appearance.

---

# 29. Color System

Vistara uses a warm, natural palette.

| Role           | Direction          |
| -------------- | ------------------ |
| Background     | Warm Ivory / Cream |
| Surface        | Soft Cream         |
| Primary        | Deep Earth Brown   |
| Secondary      | Sand / Beige       |
| Accent         | Muted Teal         |
| Main Text      | Deep Charcoal      |
| Secondary Text | Warm Gray          |
| Verified       | Soft Natural Green |
| Warning        | Muted Amber        |

The palette is inspired by natural travel environments:

```text
Sand
Earth
Cream
Sea
Nature
```

while remaining an original Vistara visual system.

---

# 30. Typography

Typography should create a premium travel feeling while remaining highly readable.

```text
H1 → Destination / Property Story
H2 → Major Sections
H3 → Cards / Components
Body → Description
Small → Metadata / Verification
```

Headings should have generous spacing and strong visual hierarchy.

---

# 31. Property Page Experience

The property page follows an information-rich structure:

```text
┌─────────────────────────────────────┐
│           HERO GALLERY              │
├─────────────────────────────────────┤
│ Property Name                       │
│ Location · Rating · Verification    │
├─────────────────────────────────────┤
│ Property Story                      │
├─────────────────────────────────────┤
│ Amenities                           │
├─────────────────────────────────────┤
│ Host                                │
├─────────────────────────────────────┤
│ Trust & Verification                │
├─────────────────────────────────────┤
│ Host Requirements                   │
├─────────────────────────────────────┤
│ Reviews                             │
├─────────────────────────────────────┤
│ Experiences                         │
├─────────────────────────────────────┤
│ Services                            │
└─────────────────────────────────────┘
```

On desktop, booking information can remain visible alongside the content.

---

# 32. Property Card Requirements

Property cards should remain clean and scannable.

Example:

```text
┌──────────────────────────────┐
│                              │
│        PROPERTY IMAGE        │
│                              │
│                         ♡    │
└──────────────────────────────┘

✓ Verified Property

Villa · North Goa

4.8 ★ (96)

₹6,500 / night
₹8,200 estimated total

Pool · Wi-Fi · Kitchen
```

The card should provide enough information for discovery without replacing the detailed property page.

---

# 33. Host Presentation

Host information should communicate identity and trust.

```text
HOST

[Profile Image]

Host Name

✓ Identity Verified
✓ Business Verified

Response Rate
98%

Response Time
Within 1 hour
```

Only applicable information should be displayed.

---

# 34. Review UI

The review experience should communicate both emotion and structured information.

```text
4.8 ★ Excellent

Cleanliness       4.9
Location          4.8
Accuracy          4.7
Communication     4.9
Value             4.6

✓ Verified Stay

"Guest experience..."

[Guest Photos]

Host Response
```

This makes reviews useful for decision-making without reducing them to a single score.

---

# 35. AI Search UI

The search interface should support both traditional and conversational search.

### Traditional

```text
Where?
Dates?
Guests?
```

### AI Search

```text
"Find me a quiet villa near the beach
for 3 nights with a pool."
```

The system converts the request into structured search criteria.

---

# 36. Destination Storytelling

Destination pages should connect accommodation with the surrounding place.

Example:

```text
EXPLORE GOA

Stay
├── Villas
├── Apartments
├── Hotels
└── Homestays

Experiences
├── Local Food
├── City Tour
├── Photography
├── Adventure
└── Culture

Services
├── Airport Pickup
├── Chef
├── Cleaning
└── Equipment Rental
```

The destination itself becomes part of the discovery experience.

---

# 37. Responsive Design

Vistara follows a mobile-first approach.

### Mobile

```text
Hero
 ↓
Property Info
 ↓
Trust
 ↓
Requirements
 ↓
Reviews
 ↓
Experiences
 ↓
Services
 ↓
Booking
```

### Desktop

```text
┌────────────────────────────────────────────┐
│ Navbar                                     │
├────────────────────────────────────────────┤
│ Hero Gallery                               │
├───────────────────────────┬────────────────┤
│ Property Information      │ Booking Card   │
│ Story                     │                │
│ Trust                     │ Price          │
│ Requirements              │ Dates          │
│ Reviews                   │ Guests         │
│ Experiences               │ Book           │
└───────────────────────────┴────────────────┘
```

---

# 38. Core User Journey

The complete Minor experience is:

```text
DISCOVER
   ↓
SEARCH
   ↓
FILTER / AI SEARCH
   ↓
VIEW PROPERTY
   ↓
UNDERSTAND PROPERTY
   ↓
CHECK REVIEWS
   ↓
CHECK VERIFICATION
   ↓
CHECK REQUIREMENTS
   ↓
CONFIRM REQUIREMENTS
   ↓
VIEW PRICE
   ↓
BOOK
   ↓
PAY
   ↓
STAY
   ↓
REVIEW / REPORT
   ↓
TRUST SIGNAL
```

---

# 39. Minor Functional Scope

The Minor must deliver a working accommodation marketplace with:

```text
✓ Authentication
✓ Guest / Host / Admin
✓ Profiles
✓ Property Management
✓ Accommodation Categories
✓ Search
✓ Filters
✓ Map
✓ Availability
✓ Booking
✓ Payment
✓ Wishlist
✓ Reviews
✓ Verified Stay
✓ Verification Foundation
✓ Trust Indicators
✓ Host Requirements
✓ Requirement Confirmation
✓ Requirement Snapshot
✓ Mismatch Reporting
✓ AI Travel Assistant
✓ Natural Language Search
✓ Basic AI Recommendation
✓ Price Breakdown
✓ Experiences
✓ Stay-related Services
✓ Notifications
✓ Dashboards
✓ Admin Management
```

---

# 40. Major Scope

The Major phase extends the Minor system with advanced capabilities.

```text
Advanced AI
      +
Advanced Recommendation
      +
Advanced Trust / Risk
      +
Fraud Detection
      +
Image / Property Intelligence
      +
Money Radar
      +
Regulatory / Compliance
      +
Real-Time Communication
      +
Travel Agency
      +
Broader Tourism Marketplace
      +
Advanced Infrastructure
```

Major examples include:

* Advanced ML recommendation
* Semantic search
* Advanced personalization
* Behaviour-based ranking
* Review anomaly detection
* Behaviour anomaly detection
* Photo/property authenticity analysis
* Advanced risk engine
* Money Radar
* Regulatory/compliance workflows
* Real-time guest-host messaging
* Travel agency functionality
* Travel packages
* Art galleries
* Museums
* Attractions
* Entertainment
* Events
* Tour operators
* Advanced microservices
* Kubernetes
* AWS
* CI/CD
* Advanced monitoring and observability

---

# 41. Functional Requirement Summary

| Module         | Requirement Prefix |
| -------------- | ------------------ |
| Authentication | FR-AUTH            |
| User/Profile   | FR-USER            |
| Property       | FR-PROP            |
| Search         | FR-SEARCH          |
| Map            | FR-MAP             |
| Booking        | FR-BOOK            |
| Payment        | FR-PAY             |
| Verification   | FR-VERIFY          |
| Trust          | FR-TRUST           |
| Requirements   | FR-REQ             |
| Reviews        | FR-REVIEW          |
| AI             | FR-AI              |
| Wishlist       | FR-WISH            |
| Experiences    | FR-EXP             |
| Services       | FR-SVC             |
| Notifications  | FR-NOTIF           |
| Dashboard      | FR-DASH            |
| Admin          | FR-ADMIN           |

---

# 42. Final Day 9 Architecture of Behaviour

```text
                         VISTARA
                            │
              ┌─────────────┼─────────────┐
              ↓             ↓             ↓
           DISCOVERY       TRUST          AI
              │             │             │
              └─────────────┼─────────────┘
                            ↓
                         PROPERTY
                            │
             ┌──────────────┼──────────────┐
             ↓              ↓              ↓
          REVIEWS      REQUIREMENTS   VERIFICATION
             │              │              │
             └──────────────┼──────────────┘
                            ↓
                          BOOK
                            ↓
                          PAY
                            ↓
                          STAY
                            ↓
                    REVIEW / REPORT
                            ↓
                      TRUST SIGNAL
                            ↓
                    FUTURE DISCOVERY
```

---

# 43. Day 9 Final Outcome

At the end of Day 9, Vistara has a defined functional contract for:

```text
USER
  ↓
UI
  ↓
FRONTEND
  ↓
API
  ↓
BACKEND
  ↓
DATABASE / SERVICES
  ↓
AI / ML SERVICES
  ↓
RESULT
  ↓
USER
```

The product experience is simultaneously defined around:

```text
FUNCTIONALITY
     +
TRUST
     +
AI
     +
REVIEWS
     +
STORYTELLING
     +
TRANSPARENCY
     +
PREMIUM UX
```

---

# 44. Final Day 9 Statement

Day 9 establishes **what Vistara does and how the user experiences it**.

The system is designed so that a user can:

> **Discover a destination → find a property → understand its story → evaluate reviews → verify trust → understand requirements → see transparent pricing → book → stay → provide verified feedback.**

The design direction combines **review depth, warm premium aesthetics, and destination storytelling** while keeping Vistara's central identity focused on:

> **AI + Trust + Verification + Transparency + Accommodation.**

**Day 9 is now complete.**

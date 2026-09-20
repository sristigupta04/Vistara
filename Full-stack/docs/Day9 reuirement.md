# Vistara — UI/UX & Product Design System

> **Don't just find a stay. Know what you're booking.**

Vistara is designed as a **trust-aware, AI-enhanced accommodation and travel platform** where discovery, detailed property information, verification, reviews, requirements, booking, and travel experiences come together in one system.

The design direction combines:

* **Moctale-inspired review & community experience**
* **Soothey-inspired calm, warm and premium visual language**
* **Abu Dhabi tourism-inspired destination storytelling and information-rich presentation**
* **Vistara's own trust, verification, AI and booking system**

The goal is not to copy any existing platform, but to take useful **design principles** from these references and create a distinct Vistara experience.

---

# 1. Design Philosophy

Vistara follows four major principles:

```text
DISCOVER
   ↓
UNDERSTAND
   ↓
VERIFY
   ↓
TRUST
   ↓
BOOK
   ↓
EXPERIENCE
   ↓
REVIEW
```

A user should never feel that they are simply browsing a collection of property cards.

The platform should help users answer:

* Where should I stay?
* What is this property really like?
* Can I trust the host?
* Is the property verified?
* Does it match the description?
* What are the actual requirements?
* What will I really pay?
* What did previous guests experience?
* What can I do around the property?

---

# 2. Visual References

## 2.1 Moctale — Review & Community Inspiration

Moctale is used as inspiration for making reviews more meaningful than a simple star rating.

Instead of:

```text
★★★★★
"Nice place."
```

Vistara will present structured guest intelligence:

```text
Overall Rating
4.8 ★

Cleanliness       4.9
Location          4.8
Accuracy          4.7
Communication     4.9
Value             4.6
```

Along with:

* Verified Stay
* Guest photographs
* Detailed review
* Review highlights
* Guest experience signals
* Host response
* Property mismatch reports
* Trust indicators

The objective is to help future guests understand **what previous guests actually experienced**.

---

# 3. Review System

Reviews are a core part of Vistara's trust architecture.

## Review Structure

```text
Guest Review
│
├── Overall Rating
│
├── Cleanliness
├── Location
├── Accuracy
├── Communication
├── Value
│
├── Written Experience
│
├── Guest Photos
│
├── Verified Stay
│
├── Host Response
│
└── Trust / Mismatch Feedback
```

## Verified Stay

A review connected to a completed booking can receive:

```text
✓ Verified Stay
```

This allows users to distinguish between verified booking experiences and other forms of feedback.

## Post-Stay Mismatch

Guests can report cases where:

```text
LISTING CLAIM
      ↓
ACTUAL EXPERIENCE
      ↓
MATCH / MISMATCH
```

For example:

* Property description differed
* Amenity unavailable
* Room condition differed
* House rule differed
* Location information was misleading
* Host requirement was different from what was shown

A mismatch report becomes part of the trust feedback system.

---

# 4. Soothey-Inspired Visual Language

Vistara will use a **warm, calm, natural and premium visual language**.

The exact design will remain original to Vistara.

## Color Direction

```text
Primary Background
Warm Ivory / Cream

Primary
Deep Earth Brown

Secondary
Sand / Beige

Accent
Muted Teal

Text
Deep Charcoal

Verified / Positive
Natural Soft Green

Warning
Muted Amber
```

### Example Palette

| Role           | Direction   |
| -------------- | ----------- |
| Background     | Warm Ivory  |
| Surface        | Soft Cream  |
| Primary        | Deep Brown  |
| Secondary      | Sand Beige  |
| Accent         | Muted Teal  |
| Main Text      | Charcoal    |
| Secondary Text | Warm Gray   |
| Verified       | Soft Green  |
| Warning        | Muted Amber |

The interface should feel:

**Warm → Calm → Premium → Trustworthy → Travel-oriented**

rather than:

**Bright → Commercial → Generic marketplace**

---

# 5. Typography

Typography should communicate premium travel information without sacrificing readability.

### Headings

Large, elegant and spacious.

Example:

```text
Stay somewhere
worth remembering.
```

### Body

Simple and highly readable.

### UI Text

Compact and functional.

Hierarchy:

```text
H1 → Destination / Property Story
H2 → Major Sections
H3 → Cards / Components
Body → Description
Small → Metadata / Verification
```

---

# 6. Abu Dhabi-Inspired Storytelling

Property and destination pages should provide **more context than a conventional booking platform**.

Instead of showing only:

```text
Image
Name
Price
Book
```

Vistara presents:

```text
Hero
  ↓
Property Story
  ↓
Location
  ↓
Experience
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

The design should make the destination feel like part of the product.

---

# 7. Property Detail Page

## Hero Section

Large immersive property imagery.

```text
------------------------------------------------
|                                              |
|              PROPERTY IMAGE                  |
|                                              |
|   ✓ Verified Property                        |
|                                              |
------------------------------------------------

Villa in North Goa

4.8 ★ 96 Reviews

₹XXXX / night
```

The hero should immediately communicate:

* Property type
* Location
* Rating
* Verification
* Price
* Main visual identity

---

# 8. Property Story

Each property can have a structured story:

```text
About this stay

A peaceful coastal villa designed for
families and small groups looking for
a private stay close to the beach.
```

Additional information:

* What makes the property special
* Who it is suitable for
* Nearby attractions
* Local context
* Host-provided description

---

# 9. Trust Section

Trust information should be highly visible.

```text
YOUR TRUST CHECK

✓ Host Identity Verified
✓ Property Verified
✓ Business Verified
✓ Documents Checked

Trust Status: Verified
```

If something requires additional review:

```text
⚠ Verification Under Review
```

Important:

> **SUSPICIOUS does not automatically mean FRAUD.**

It means that additional review or investigation may be required.

---

# 10. Host Section

The host should be presented as a person/business rather than just a name.

```text
HOST

[Profile Image]

Rahul
Host since 2026

✓ Identity Verified
✓ Business Verified

Response rate
98%

Response time
Within 1 hour
```

Depending on the property, host information can include:

* Host profile
* Verification status
* Response rate
* Response time
* Number of properties
* Hosting information
* Business information where applicable

---

# 11. Host Requirements

A major Vistara feature.

Before booking, guests should clearly see:

```text
HOST REQUIREMENTS

✓ Government ID required
✓ Maximum 4 guests
✓ No smoking
✓ No parties
✓ Check-in after 2 PM
✓ Check-out before 11 AM
```

The guest explicitly confirms:

```text
☑ I have read and agree to the requirements.
```

This confirmation becomes associated with the booking.

---

# 12. Requirement Snapshot

At booking time, the system stores the requirements shown to the guest.

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

This provides a historical reference if the property requirements later change.

---

# 13. Trust Feedback Loop

Vistara's review system connects directly to its trust system.

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

This makes reviews part of the platform's **trust infrastructure**, rather than just a rating feature.

---

# 14. AI Experience

AI should feel integrated into the product instead of being an isolated chatbot.

## AI Travel Assistant

Example:

> "I want a peaceful beach stay in Goa for 4 people under ₹8,000 per night, preferably with a pool and good reviews."

AI extracts:

```text
Destination → Goa
Guests → 4
Budget → ₹8,000
Preference → Peaceful
Location → Beach
Amenity → Pool
Review Preference → Good
```

Then converts the request into a search.

---

# 15. AI + Trust

Vistara's AI layer should not only recommend based on price or popularity.

It can eventually consider:

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
```

Result:

```text
PERSONALIZED + TRUST-AWARE DISCOVERY
```

---

# 16. Search Experience

Search should support both traditional and natural-language discovery.

### Traditional

```text
Where?
Dates?
Guests?
```

### Natural Language

```text
"Find me a quiet villa near the beach
for 3 nights with a pool."
```

The interface should allow users to move naturally from:

```text
SEARCH
  ↓
FILTER
  ↓
COMPARE
  ↓
UNDERSTAND
  ↓
VERIFY
  ↓
BOOK
```

---

# 17. Property Cards

Property cards should remain visually clean.

```text
┌──────────────────────────────┐
│                              │
│        PROPERTY IMAGE        │
│                              │
│  ♡                           │
└──────────────────────────────┘

✓ Verified Property

Villa · North Goa

4.8 ★ (96)

₹6,500 night
₹8,200 estimated total

Pool · Wi-Fi · Kitchen
```

Avoid putting too much information directly on the card.

Detailed information belongs on the property page.

---

# 18. Destination Experience

Vistara should not stop at accommodation.

A destination page can include:

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
├── Photography Walk
├── Adventure
├── Cultural Experience
└── Nature Experience

Services
├── Airport Pickup
├── Chef
├── Cleaning
├── Photography
└── Equipment Rental
```

This gives Vistara a broader travel experience without moving Travel Agency features into Minor.

---

# 19. Experiences — Minor

The Minor version can support basic experiences:

* Local food experience
* City tour
* Photography walk
* Adventure activity
* Cultural experience
* Workshop
* Nature experience
* Local guide

These should be integrated into destination and property discovery.

---

# 20. Services — Minor

Basic stay-related services:

* Cleaning
* Airport pickup
* Chef
* Photography
* Equipment rental
* Local guide
* Other relevant stay services

---

# 21. Price Transparency

The design should avoid hiding the actual cost.

Instead of:

```text
₹5,000/night
```

show:

```text
Price Breakdown

Stay                 ₹5,000
Cleaning             ₹800
Taxes                ₹900
────────────────────────────
Estimated Total      ₹6,700
```

The full **Money Radar** intelligence belongs to the Major phase.

---

# 22. Booking Experience

Booking should follow a clear sequence:

```text
SELECT PROPERTY
      ↓
SELECT DATES
      ↓
SELECT GUESTS
      ↓
CHECK AVAILABILITY
      ↓
VIEW REQUIREMENTS
      ↓
CONFIRM REQUIREMENTS
      ↓
VIEW PRICE
      ↓
PAYMENT
      ↓
BOOKING CONFIRMED
```

The UI should avoid unnecessary friction.

---

# 23. Dashboard Design

## Guest Dashboard

```text
My Trips
Upcoming
Past Trips
Wishlist
Reviews
Profile
AI Travel Assistant
```

## Host Dashboard

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

## Admin Dashboard

```text
Users
Properties
Bookings
Verification
Reports
Trust Signals
Suspicious Cases
Reviews
Analytics
```

---

# 24. Navigation System

Primary navigation:

```text
VISTARA

Stay
Explore
Experiences
Services

Search

Wishlist

Trips

Profile
```

For desktop:

```text
Logo
│
├── Stays
├── Explore
├── Experiences
├── Services
│
├── Search
│
└── Profile
```

For mobile, navigation becomes simplified.

---

# 25. Design Components

The design system should use reusable components.

```text
/components

├── Navbar
├── SearchBar
├── SearchFilters
├── PropertyCard
├── PropertyGallery
├── Rating
├── ReviewCard
├── ReviewSummary
├── VerificationBadge
├── TrustCard
├── RequirementCard
├── HostCard
├── PriceBreakdown
├── BookingCard
├── ExperienceCard
├── ServiceCard
├── DestinationCard
├── AIChat
├── Notification
└── DashboardCard
```

---

# 26. Trust UI States

Every verification-related component should have clear states.

```text
PENDING
   ↓
VALIDATING
   ↓
RISK ANALYSIS
   ↓
┌───────────┬──────────────┐
↓           ↓              ↓
VERIFIED   REJECTED     REVIEW REQUIRED
```

UI examples:

```text
✓ Verified

⏳ Verification in progress

⚠ Additional review required

✕ Verification rejected
```

The system should never use alarming language without context.

---

# 27. Responsive Design

Vistara must be designed mobile-first.

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
Booking
```

### Desktop

```text
┌──────────────────────────────────────────┐
│ Navbar                                   │
├──────────────────────────────────────────┤
│ Hero Gallery                             │
├──────────────────────────┬───────────────┤
│ Property Information     │ Booking Card  │
│ Story                    │               │
│ Trust                    │ Price         │
│ Requirements             │ Dates         │
│ Reviews                  │ Guests        │
│ Experiences              │ Book          │
└──────────────────────────┴───────────────┘
```

---

# 28. Design System Principle

Vistara should feel:

```text
        PREMIUM
           +
        NATURAL
           +
        DETAILED
           +
        TRUSTWORTHY
           +
        INTELLIGENT
           +
        HUMAN
```

Not:

```text
Generic Airbnb Clone
```

---

# 29. Minor vs Major Design Scope

### Minor

```text
✓ Complete accommodation marketplace
✓ Warm premium UI
✓ Detailed property pages
✓ Structured reviews
✓ Verified Stay
✓ Verification indicators
✓ Host requirements
✓ Requirement confirmation
✓ Requirement snapshot
✓ Mismatch reporting
✓ AI Travel Assistant
✓ Natural-language search
✓ Basic AI recommendation
✓ Experiences
✓ Stay-related services
✓ Price breakdown
✓ Guest / Host / Admin dashboards
```

### Major

```text
→ Advanced AI recommendation
→ Semantic search
→ Advanced personalization
→ Fraud detection
→ Advanced trust/risk engine
→ Image authenticity analysis
→ Money Radar
→ Regulatory / compliance system
→ Real-time guest-host messaging
→ Travel Agency
→ Travel packages
→ Art Galleries
→ Museums
→ Attractions
→ Entertainment
→ Events
→ Tour Operators
→ Advanced tourism marketplace
→ Kubernetes / AWS
→ Advanced microservices
→ Advanced observability
→ CI/CD
```

---

# 30. Overall Product Experience

The final Vistara experience should connect:

```text
                  VISTARA
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
     DISCOVERY     TRUST         AI
        │            │            │
        └────────────┼────────────┘
                     ↓
                  PROPERTY
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
    REVIEWS     REQUIREMENTS   VERIFICATION
        │            │            │
        └────────────┼────────────┘
                     ↓
                   BOOK
                     ↓
                   STAY
                     ↓
             REVIEW / REPORT
                     ↓
               TRUST SIGNAL
                     ↓
             BETTER DISCOVERY
```

---

# 31. Final Design Statement

Vistara's design is built around the idea that **travel discovery should be beautiful, but trust should be visible**.

The platform combines:

**Moctale-inspired review depth**

with

**Soothey-inspired warm visual calmness**

and

**Abu Dhabi-inspired destination storytelling**

while adding Vistara's own:

**AI + Verification + Trust + Requirements + Transparency + Booking system.**

The final product should feel like a **premium travel platform where users can explore visually, understand deeply, verify confidently, and book transparently.**

> **Vistara — Don't just find a stay. Know what you're booking.**

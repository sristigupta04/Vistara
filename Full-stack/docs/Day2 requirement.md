# 3.8 Host Requirements & Guest Confirmation

Hosts can define specific requirements and conditions that guests should know before making a booking.

### Host can specify:

* Maximum number of guests
* Age-related requirements where applicable
* Valid ID requirement
* Pet policy
* Smoking policy
* Check-in/check-out conditions
* Property-specific rules
* Required documents where legally/operationally appropriate
* Other important stay conditions

### Guest Flow

The guest must be able to view the host requirements before completing a booking.

```text
Property
   ↓
Host Requirements
   ↓
Guest Reviews Requirements
   ↓
Guest Confirms
   ↓
Booking
```

The guest will explicitly confirm that they have read and understood the applicable requirements.

Example:

```text
Host Requirements

✓ Maximum 4 guests
✓ Valid ID required
✓ No smoking
✓ No pets
✓ Check-in: 2 PM – 10 PM

☑ I have read and agree to the host requirements.

        [ Confirm & Continue ]
```

The confirmation should be associated with the booking.

---

# 3.9 Requirement Snapshot

The system should preserve the requirements that were applicable **at the time of booking**.

This is important because a host may modify their requirements after a booking has already been created.

```text
Host Requirements
       ↓
Booking Created
       ↓
Requirement Snapshot Stored
       ↓
Guest Confirmation Recorded
```

This allows the platform to determine what the guest actually agreed to when the booking was made.

---

# 3.10 Stay Experience & Requirement Mismatch

After check-in/stay, the guest can report if the actual property experience significantly differs from the information or requirements presented during booking.

Example:

```text
Listed / Confirmed
       ↓
Actual Stay
       ↓
Compare Experience
       ↓
Match / Mismatch
```

Possible mismatch categories:

* Property information mismatch
* Missing advertised amenity
* Different property condition
* Incorrect check-in information
* Host requirement mismatch
* Property access issue
* Other reported issue

The guest may provide:

* Description
* Photos/evidence where appropriate
* Relevant booking information

---

# 3.11 Issue Reporting & Trust Review

Reported mismatches will be connected to the platform's Trust & Safety system.

```text
Guest
  ↓
Report Issue
  ↓
Report / Case System
  ↓
Trust & Risk Analysis
  ↓
Admin Review (if required)
  ↓
Resolution
```

Repeated or significant reports may become signals for the Trust/Risk system.

The system should distinguish between:

* A normal complaint
* A verified mismatch
* A disputed claim
* A suspicious/repeated pattern

A report should **not automatically classify a host or property as fraudulent**.

---

# 3.12 Post-Stay Review

After the stay, eligible guests can provide a review based on their actual experience.

The review may cover:

* Overall experience
* Accuracy of listing
* Cleanliness
* Location
* Communication
* Check-in
* Property condition
* Whether important expectations were met

The platform can use verified booking and reported experience data as additional trust signals.

```text
Completed Booking
       ↓
Actual Stay
       ↓
Guest Feedback
       ↓
Review
       +
Issue Report (if required)
       ↓
Trust Signals
```

---

# 3.13 Vistara Expectation-to-Experience Trust Loop

This feature creates a dedicated trust cycle in Vistara:

```text
       HOST
        │
        ▼
Define Requirements
        │
        ▼
Guest Sees Requirements
        │
        ▼
Guest Confirms
        │
        ▼
     BOOKING
        │
        ▼
    ACTUAL STAY
        │
        ▼
 ┌──────┴────────┐
 │               │
 ▼               ▼
MATCH         MISMATCH
 │               │
 ▼               ▼
 REVIEW       REPORT
 │               │
 └──────┬────────┘
        ▼
 TRUST / RISK SIGNAL
        │
        ▼
   ADMIN REVIEW
   (if required)
```

This feature is designed to improve **expectation clarity, transparency, accountability, and trust** between guests and hosts.

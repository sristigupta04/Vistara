# Vistara — Day 9: Functional Requirements

> Corrected — verification section rewritten to match the property/photo verification model, not ID-document upload.
> Traceable to Day 3's gaps: Verification (Gap 1), Requirements (Gap 2), Mismatch Reporting (Gap 3), Review/Review Intelligence (Gap 4), Price (Gap 5), Recommendation (Gap 6).

## 1. Authentication
- **FR-AUTH-01**: Guest/Host/Admin can register with name, email, password. Acceptance: account created only with valid input.
- **FR-AUTH-02**: Users log in via email/password, receive a session. Acceptance: invalid credentials rejected.
- **FR-AUTH-03**: Role-based access restricts endpoints/UI by role.

## 2. Property Management
- **FR-PROP-01**: Host can create a property listing (name, description, category, location, price, capacity, amenities, images).
- **FR-PROP-02**: Host can edit/update a listing.
- **FR-PROP-03**: System maintains availability per property, preventing double-booking.

## 3. Search
- **FR-SEARCH-01**: Guest can search by location, dates, guest count.
- **FR-SEARCH-02**: Guest can filter by price, category, amenities, verification status.
- **FR-SEARCH-03** (Phase 8, secondary): Guest can enter a natural-language query; system extracts structured parameters via LLM API, falls back to manual filters if unavailable.

## 4. Booking & Payment
- **FR-BOOK-01**: System checks availability before allowing booking creation.
- **FR-BOOK-02**: Guest must confirm host requirements before booking completes.
- **FR-BOOK-03**: Booking has status: PENDING / CONFIRMED / CANCELLED / COMPLETED.
- **FR-PAY-01**: Guest initiates payment via Razorpay (test mode for MVP).
- **FR-PAY-02**: Payment status tracked and tied to booking status.

## 5. Verification (Corrected)
- **FR-VERIFY-01**: On property creation, submitted images are queued for automated verification checks (duplicate detection, consistency analysis). No host identity document is collected or required — explicit project exclusion.
- **FR-VERIFY-02**: Verification status follows PENDING → PROCESSING → VERIFIED / FLAGGED (flagged = review required, not "rejected" or "fraud" — matches Day 10's usability language rule).
- **FR-VERIFY-03**: FLAGGED properties enter an admin review queue; admin decides VERIFIED or REQUIRES_CHANGES.
- **FR-VERIFY-04**: Verification status is visibly displayed on the listing (badge, per Day 10 usability language rules).

## 6. Requirements
- **FR-REQ-01**: Host defines requirements (guest limit, ID required, pet/smoking policy, check-in/out rules).
- **FR-REQ-02**: Requirements are displayed to guest before booking.
- **FR-REQ-03**: Guest must explicitly check "I have read and agree" before booking proceeds.
- **FR-REQ-04**: The exact requirements shown at booking time are stored as an immutable snapshot on the booking record.

## 7. Reviews & Mismatch Reporting
- **FR-REVIEW-01**: Guest can review only after a completed booking.
- **FR-REVIEW-02**: Reviews tied to a completed booking display a "Verified Stay" tag.
- **FR-REVIEW-03**: Review includes overall rating + structured sub-ratings.
- **FR-REVIEW-04** (Phase 7): Review text feeds a sentiment/aspect analysis pipeline producing a structured property-level summary.
- **FR-MISMATCH-01**: Guest can file a mismatch report post-stay, categorized by type.
- **FR-MISMATCH-02**: Mismatch reports enter the admin review queue and feed the trust/risk model as a signal (Phase 6).

## 8. Trust & Risk (Phase 6)
- **FR-RISK-01**: System computes a trust/risk indicator per property/host from booking behavior, mismatch report frequency, and verification outcomes.
- **FR-RISK-02**: Risk indicator is surfaced to admin, not directly to guests as a raw score — guests see the existing verification badge (FR-VERIFY-04) and Verified Stay tags, not a numeric risk figure.

## 9. Recommendation & Personalization (Phase 5, 8)
- **FR-REC-01**: System returns ranked property recommendations based on content similarity (Phase 5 baseline).
- **FR-REC-02** (Phase 8): Ranking incorporates logged user interaction data (search, views, saves) where available; falls back to content-based ranking for new users (cold start).

## 10. Price
- **FR-PRICE-01**: System displays a breakdown (base price + cleaning fee + taxes = total) before payment.

## 11. Dashboards
- **FR-DASH-01**: Guest dashboard shows bookings, wishlist, reviews.
- **FR-DASH-02**: Host dashboard shows properties, bookings, verification status, requirements.
- **FR-DASH-03**: Admin dashboard shows verification queue, mismatch report queue, risk-flagged cases, user/property lists.

## 12. Parking (New — Gap 7)
FR-PARK-01: Owner can list a parking space (location, availability window, price).
FR-PARK-02: Guest can search parking spaces near a property or destination.
FR-PARK-03: Guest can book a parking space; status follows PENDING/CONFIRMED/CANCELLED/COMPLETED, payment via existing Payment module.
## 13.Experiences (New — Gap 8)
FR-EXP-01: Provider can create an experience listing (title, description, location, duration, price, availability).
FR-EXP-02: Guest can discover experiences tied to a destination or a booked property.
FR-EXP-03: Guest can book an experience; payment reuses the existing Payment module.
FR-EXP-04: Guest can review a completed experience, reusing the Review module's rating structure.
 
## conculsion

Verification requirements now match the roadmap's explicit exclusion of ID-upload verification, and trust/risk, recommendation, and review intelligence are represented as real, phased requirements rather than omitted.

Next: Day 10 — Non-functional requirements (unaffected by this correction, stands as originally written).
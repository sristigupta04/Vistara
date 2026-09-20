# Vistara — Day 6: Proposed Solution

> Track: Full Stack / Product | Phase 1 — Research & Scope | Day 6/90
> Translates Day 5's objectives into platform modules. Still no tech decisions — that's Phase 2.

## 1. Solution Outline

Vistara is a standard accommodation marketplace (listing, search, booking, payment) with a **Trust Layer** and an **Intelligence Layer**, each module tracing to a specific Day 3 gap.

```
CORE MARKETPLACE          TRUST LAYER                INTELLIGENCE LAYER (phased)
----------------          -----------                ---------------------------
Property listing          Property/photo             Recommendation (Phase 5)
Search & filters          verification                Trust/risk scoring (Phase 6)
Availability               Requirement + snapshot      Review intelligence (Phase 7)
Booking                    Mismatch reporting          Trust-aware ranking (Phase 8)
Payment                    Structured reviews
```

## 2. Module Breakdown

### 2.1 Verification Module (Gap 1)
- Automated on property image upload: duplicate detection, listing-consistency checks
- Status: PENDING -> PROCESSING -> VERIFIED / FLAGGED
- Flagged cases enter an admin review queue (human-in-loop, not full manual review of everything)
- No ID-document collection — explicit exclusion

### 2.2 Requirement Module (Gap 2)
- Host defines requirements at listing time (max guests, ID required, pet/smoking policy, check-in/out rules)
- Guest must explicitly confirm before booking completes
- Snapshot of requirements stored permanently against the booking, immutable even if the listing later changes

### 2.3 Mismatch Reporting Module (Gap 3)
- Guest can file a report post-stay, separate from a public review
- Categorized (description mismatch, amenity unavailable, condition issue, etc.)
- Feeds the trust/risk model as a behavioral signal (Phase 6)

### 2.4 Review Module (Gap 4)
- Star rating + structured sub-ratings (cleanliness, accuracy, communication, value)
- "Verified Stay" tag shown only when tied to a completed booking
- Aspect/sentiment summarization is a Phase 7 addition, not MVP-day-one

### 2.5 Price Module (Gap 5)
- Basic breakdown shown before payment: base price + cleaning fee + taxes = total
- No dynamic price-comparison intelligence (Money Radar) — logged as future scope

### 2.6 Trust-Aware Discovery (Gap 6, secondary/later)
- Basic search + filters ship first (Phase 3-4)
- Recommendation (Phase 5) and trust/risk-aware ranking (Phase 8) layer on top once the underlying models exist
- Natural-language search is a small convenience feature within Phase 8, not a headline MVP feature

## 3. What This Solution Does NOT Include

Unchanged: destination/"Explore" discovery, hidden gems, guide marketplace, trip planner, parking marketplace, local food discovery, business/certificate verification, real-time messaging. All logged in `Vistara-Major-Future-Roadmap.md`.

## 4. Day 6 Conclusion

> **The solution is a marketplace plus a trust layer (verification, requirements, mismatch reporting, structured reviews) plus a phased intelligence layer (recommendation, risk scoring, review intelligence, trust-aware ranking) — six modules, each tracing directly to one of Day 3's six gaps.**

Next: Day 7 — Differentiation, confirming this solution against competitors one more time before locking the USP.
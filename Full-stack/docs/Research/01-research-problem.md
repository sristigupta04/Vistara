# Vistara — Day 1: Problem Space & AI/ML Research

> Scope note: This document covers the accommodation booking marketplace only. Trip planning, group travel, travel agency tours, coupons, and location-radius discovery are intentionally excluded — see `Vistara-Major-Future-Roadmap.md`. If a new idea shows up while reading this, it goes in that file, not here.

---

## 1. Day 1 Objective

Understand, before deciding anything:

* What problems travellers face when discovering and booking accommodation
* What problems hosts face when listing and managing properties
* What problems exist around trust, verification, and reviews
* What problems exist around price transparency
* Where AI can genuinely help — not where AI sounds impressive
* What data Vistara could realistically generate and use

Day 1 does **not** decide final features, architecture, tech stack, or Minor/Major split. That happens later, on schedule (Day 8 freeze, per the existing roadmap).

---

## 2. The Core Problem

Existing platforms — Airbnb, Vrbo, Booking.com, Kayak — already solve **discovery**: search, filter, sort, compare, book. That part of the problem is mature and well-served.

What they solve less well:

> **Once a guest finds a listing, how do they know it's actually what it claims to be — and that the host is who they say they are?**

Guests currently have to:
- Trust photos that may be old, staged, or not of the actual unit
- Trust reviews that may not distinguish verified stays from anything else
- Trust host claims about amenities, rules, and property condition with no recourse if reality differs
- Guess whether a "too good" price is a deal or a red flag

This is the problem Vistara focuses on: **making trust visible instead of assumed**, on top of a normal accommodation marketplace.

---

## 3. Traveller Problems

### 3.1 Discovery overload
Standard search flow:
```
Destination → Dates → Filters → Sort → Open listing → Compare → Back → Repeat
```
This is functional but effortful. A guest with a specific need ("quiet place, parents, near temples, under ₹5,000") still has to manually translate that into filters.

### 3.2 Trust uncertainty
- Is this listing accurate?
- Is this host real?
- Will the property match the photos?
- What happens if it doesn't?

### 3.3 Review noise
Star ratings compress everything into one number. A guest can't easily tell *why* a place is rated 4.6 — good location but bad communication? Clean but overpriced?

### 3.4 Price uncertainty
A guest sees ₹3,000/night with no context for whether that's fair for the category, location, and amenities on offer.

### 3.5 Requirement ambiguity
House rules and host requirements are often buried in listing text, discovered only after booking, leading to disputes.

---

## 4. Host Problems

- Building credibility as a new/unverified host with no track record
- No structured way to set and enforce requirements (guest limits, ID, pet policy) before a booking is confirmed
- Disputes with guests over "what was agreed" with no record to point to
- Managing availability, pricing, and bookings without losing track of details
- No visibility into whether a guest inquiry is legitimate

---

## 5. Trust & Verification Problems

- No standard way for a platform to confirm a property listing is accurate — genuine photos, consistent information, not duplicated from elsewhere
- "Suspicious" activity needs a way to be flagged without falsely branding someone as fraudulent
- Guests have no visibility into *what* was actually verified about a property
- No mechanism connects a guest's actual stay experience back into the trust system — reviews and verification are currently separate

> Note: host/guest identity-document verification is explicitly out of scope for this project. Trust here means property/listing verification and behavior-based risk signals — not ID upload.

---

## 6. Price Transparency Problems

- Listed price often excludes cleaning fees, taxes, service charges until late in the booking flow
- No easy way to tell if a price is reasonable relative to similar nearby listings
- Guests have no help understanding *why* a place costs what it costs

---

## 7. Review System Problems

- Reviews aren't tied to verified completed stays, so anyone could theoretically leave one
- No structured breakdown (cleanliness, accuracy, communication, value) — just a single score
- No mechanism for reporting when a stay didn't match the listing, separate from a public review

---

## 8. Competitor Reference Points

Researched for **specific UX patterns**, not for feature copying:

| Platform | What we're taking |
|---|---|
| **Vrbo** | Clean property-type categorization (villas, homes, cabins) suited to destination-style stays |
| **Kayak** | Fast, low-friction comparison and filtering UX |
| **Moctale** | Reviews as structured, multi-dimension guest intelligence rather than a single star average |
| **Soothey** | Warm, calm, premium visual language instead of a generic marketplace look |
| **Airbnb / Booking.com** | Baseline for what's already table-stakes (search, filters, reviews, messaging) — confirms these are *not* differentiators for Vistara |

None of these are being cloned. Each contributes one specific, nameable pattern.

---

## 9. AI/ML Opportunity Map

Opportunities identified, not committed:

| Problem | Possible AI/ML angle |
|---|---|
| Search overload | Natural-language query → structured search parameters |
| Too many similar listings | Basic recommendation (rule-based or content-based to start) |
| Review noise | Structured review dimensions (already product-level, not ML-dependent for MVP) |
| Price uncertainty | Comparative price context ("similar listings: ₹X–Y") — rule-based initially |
| Trust/risk signals | Risk classification from booking/account behavior patterns — core 90-day work, Phase 6 |
| Photo authenticity | Image consistency/duplicate detection — core 90-day work, Phase 7 |
| Review depth | Sentiment/aspect extraction from review text — core 90-day work, Phase 7 |

The point of this table, corrected: some of Vistara's trust layer (requirement snapshot, mismatch reporting) is a product/data-model problem, not an ML problem. But property verification, risk scoring, and review intelligence genuinely are ML problems, and they are scheduled as real, in-scope work across the 90-day plan (Phases 5–8) — not deferred. Keep that distinction honest going into Day 11 so effort is allocated correctly, not under- or over-stated.

---

## 10. Data Opportunity Map

What Vistara could generate through normal usage, to inform later data/ML strategy (Day 12):

```
Search queries → destination, dates, budget, preferences
Property views, saves, comparisons
Bookings, cancellations
Reviews (structured, per-dimension)
Verification outcomes (auto-processed on image upload)
Mismatch reports
```

This becomes the seed for recommendation and trust-signal work later — but is not needed to ship a working MVP.

---

## 11. What Day 1 Deliberately Excludes

To keep this document usable instead of becoming another 40-section sprawl:

- No feature list (that's Day 8, after Day 2–7 narrow it down)
- No architecture or tech decisions
- No AI trip planning, group travel, travel agency, location-radius discovery, coupons — logged separately, not researched here
- No Minor/Major classification

---

## 12. Day 1 Conclusion

The problem Vistara is built to solve:

> **Accommodation discovery already works well on existing platforms. Trust doesn't. Vistara's job is to make trust — in the host, the property, and the listing itself — visible and verifiable, without turning the product into a 15-feature platform before a single booking has ever gone through it.**

Next: **Day 2 — Competitor analysis**, evaluating Airbnb, Vrbo, Booking.com, Kayak, Agoda specifically against this trust problem (not general feature parity).
# Vistara — Day 12: Dataset & API Strategy

> Corrected. The previous version incorrectly deferred ML dataset work (USER_EVENT, trust signals) to "Major," contradicting the corrected Day 11/16/20, where this data collection is Phase 3-7 work.

## 1. Primary Database
- **Neon PostgreSQL** + **Prisma ORM** — application data across all 18 tables defined in Day 16

## 2. Core Entities (Corrected — Matches Day 16)
```
User, HostProfile, GuestProfile
Property, PropertyImage (with perceptualHash, verification fields), Amenity, Availability
Booking, Payment
Review, ReviewSummary
Verification
Requirement, RequirementSnapshot
MismatchReport
TrustScore
UserEvent
```
Genuinely deferred: `AIConversation` (no persistent chat feature planned), `Experience`, `Service` (experiences/services marketplace excluded — see `Vistara-Major-Future-Roadmap.md`).

## 3. External APIs

| Need | Choice | Why |
|---|---|---|
| Maps/Geocoding | Google Maps Platform (locked, Day 18) | India-appropriate free tier, reliable geocoding |
| Payment | Razorpay (test mode) | India-focused, well-documented, order/webhook flow |
| NL search parsing (Phase 8 only) | Configurable LLM provider via env vars | Avoids vendor lock-in for the one *convenience* feature — not a substitute for the four ML components below, which are built in-house |
| Image storage | S3-compatible object storage | Standard, avoids storing binaries in Postgres |

**The four core ML components (recommendation, trust/risk, review intelligence, photo verification) are not external APIs** — they're built and served by the project's own FastAPI ML service (Day 15), trained on data this platform generates.

**Explicitly not needed:** Weather API, OpenSearch/Elasticsearch (Postgres search is sufficient at this scale), any third-party identity/business registry API (ID-upload and business verification are excluded entirely per project scope).

## 4. Seed Data Strategy
- 30–50 seed properties across 3–5 Indian destinations — enough to support early testing of all four ML components (Day 11's data-sufficiency check), not oversized for a thesis demo
- Clearly labeled as development/demo data, not real user content
- USER_EVENT logging starts from Phase 3-4 UI/backend work (Day 22-42), so real interaction data exists by the time Phase 5 (Day 43) begins

## 5. Data Privacy
- No plaintext passwords, no payment credentials stored
- No identity documents collected at all — not a privacy control, a scope exclusion (property/photo verification only)
- USER_EVENT data used only for recommendation/personalization features already defined in FRs — not repurposed without a documented reason

## 6. Day 12 Conclusion

> **Data strategy matches Day 16's corrected schema exactly: 18 tables, four in-house ML components fed by USER_EVENT and platform-generated data, one small external LLM dependency for NL search, Razorpay for payment, Google Maps for location. Nothing here is "Major-phase, deferred" — every table and every data source has a phase and a day assigned.**

Next: **Day 13 — Research conclusion**, synthesizing Days 1–12.
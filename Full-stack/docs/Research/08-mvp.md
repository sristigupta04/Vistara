# Vistara — Day 8: MVP Definition & Scope Freeze

> Corrected version — see `Correction-Note.md` for what changed and why. This freeze now matches the project's own 90-Day Roadmap PDF instead of contradicting it.

## 1. Core Principle

The 90-day delivery has two horizons: a **working transactional loop** (search → book → pay → review), demoable by Day 42 (Phase 4 checkpoint), and a **complete intelligent platform** (recommendation, trust/risk scoring, review intelligence, photo verification) layered on top through Phase 5–8, complete by Day 90. Both are "in scope" — they're just sequenced, not split into "MVP" and "someday."

## 2. Scope — Final (Corrected)

### Marketplace (Phase 3–4, working by Day 42)
- Auth (guest/host/admin roles)
- Property listing (create/edit, images, category, price, capacity, amenities)
- Search + filters (location, dates, guests, price, category)
- Availability calendar
- Booking creation + status (pending/confirmed/cancelled/completed)
- Payment (Razorpay, test mode)
- Basic reviews (star + structured sub-ratings)

Supply-Side Modules (Phase 4, added on explicit scope decision — Gaps 7-8)
Parking: owner lists a parking space (location, availability, price); guest searches/books near a property or destination. Basic listing + booking only — no real-time occupancy sensors, no dynamic pricing.
Experiences: provider lists a local experience (title, description, location, duration, price, availability); guest discovers/books alongside their stay. Reuses Payment and Review infrastructure. Basic marketplace only — no multi-day packages.

### Trust Layer (Phase 4 foundation, ML built out Phase 6–7)
- **Property/photo verification** — duplicate image detection and listing-consistency checks (ML, Phase 7). **Not** host ID-document upload — that is explicitly out of scope per the roadmap.
- Host requirements definition, guest confirmation, requirement snapshot (Phase 4)
- Mismatch reporting (Phase 4), feeding the risk model as a signal (Phase 6)
- Trust/risk score, ML-based, combining booking behavior + mismatch reports + photo-verification outcomes (Phase 6)
- Review intelligence — sentiment/aspect extraction, structured summaries (Phase 7)
- Admin review queue for flagged cases (human-in-loop, not full manual review of every submission)

### Intelligence Layer (Phase 5–8)
- Recommendation (baseline content-based model, Phase 5)
- Trust/risk scoring (Phase 6)
- Review intelligence (Phase 7)
- Photo/property verification (Phase 7)
- Personalization, ranking, explainability, cold-start handling (Phase 8)
- Natural-language search parsing (LLM-based, optional convenience layer within Phase 8, not the headline AI feature)

### Supporting
- Basic price breakdown (base + cleaning + tax = total)
- Guest/Host/Admin dashboards
- Basic notifications (in-app; email optional)

## 3. Explicitly Out of Scope (All 90 Days)

- ID-document/identity upload verification (explicit roadmap exclusion)
- Business/certificate verification
- Experiences and services marketplace
- Money Radar (advanced price intelligence beyond basic breakdown)
- Regulatory/compliance tracking
- Real-time messaging
- Trip planning, group travel, travel agency features
- Kubernetes/advanced infrastructure, auto-scaling

See `Vistara-Major-Future-Roadmap.md` for these as deliberate future direction.

## 4. Reality Check for a 2-Person Team

This is a full-stack build (Phase 3–4) plus four real ML components (Phase 5–7) plus a personalization/ranking layer (Phase 8) — substantial for two people, but this is exactly what the team's own 90-day roadmap already scoped and sequenced correctly. The ML partner's workload is concentrated in Phase 5–8, not absent during Phase 3–4 (see Day 20 for their Phase 3–4 preparation tasks).

## 5. Day 8 Conclusion

> **Scope = full transactional marketplace + property/photo verification + requirement snapshot + mismatch reporting + review intelligence + recommendation + trust/risk scoring + personalization, delivered across 90 days in the phases the roadmap already defines. No feature is "deferred indefinitely" — everything either has a phase and days assigned, or is explicitly excluded and logged in the future-roadmap file.**

Next: Day 9 — Functional requirements (corrected verification section).
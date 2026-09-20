# Vistara — Day 10: Non-Functional Requirements

> Kept proportionate to a 2-person team building a demoable thesis MVP — not an enterprise SLA document. Depth is intentionally limited; a bloated NFR doc at this stage is itself a scope-discipline failure (see architecture reviews from prior docs).

## 1. Security (Critical — do not cut)
- Passwords hashed, never stored plain text
- Role-based authorization enforced server-side (not just hidden in UI)
- Input validation on all user-submitted data (registration, listings, bookings, reviews, requirements)
- Sensitive data (verification/risk analysis results) access-restricted by role
- API keys/secrets in environment variables, never hardcoded or committed

## 2. Data Integrity (Critical)
- Booking creation must be atomic against availability checks — no double-booking
- Requirement snapshot, once stored on a booking, is immutable even if the host later edits the listing
- Payment status must be validated against the provider before marking a booking paid

## 3. Performance (Targets, not guarantees)
- Normal CRUD APIs: under ~500ms
- Search: under ~1s
- AI search (NL query parsing): async/non-blocking; core search must work if AI is slow or down
- ML service calls (recommendation, risk score, review summary, photo verification): async where the UI allows it (e.g., photo verification runs in the background after upload, not blocking listing creation); backend never leaves a user-facing request hanging on a slow model response

## 4. Reliability
- AI service failure must not block core booking flow (fallback to manual filters)
- ML service failure (recommendation/risk/review/photo) must degrade gracefully — e.g., search still works without recommendation ranking, a listing still publishes if photo verification is pending
- Payment provider failure handled gracefully with clear guest-facing error, no silent booking creation without payment confirmation

## 5. Testing (Minimum viable, not exhaustive)
- Critical flows tested: registration/login, booking creation, payment, photo verification processing, requirement confirmation, review creation
- Manual or lightweight automated testing acceptable given team size — full E2E suite is not required for MVP

## 6. Deployment
- Dockerized for local development (Docker Compose)
- Basic cloud deployment sufficient for demo (no Kubernetes, no auto-scaling — that's Major)

## 7. Usability
- Verification status uses clear, non-alarming language (Verified / Pending / Review Required — never "Suspicious" shown raw to guests)
- Booking flow shows price, requirements, and dates clearly before payment — no hidden steps

## 8. What's Deliberately Not Specified Here
- Detailed observability stack (Prometheus/Grafana/OpenTelemetry) — Major
- Advanced caching strategy — Redis used only where it clearly helps (sessions, rate limiting), not architected in depth for MVP
- Formal backup/recovery SLAs — noted as a future need, not specified now

## 9. Day 10 Conclusion

Security and data integrity are non-negotiable even for a student MVP — a booking platform mishandling payment status or double-booking undermines the entire trust thesis. Everything else here is scaled to match actual team capacity, not aspirational infrastructure.

Next: **Day 11 — ML research**, choosing realistic methods for each of Vistara's four ML components.
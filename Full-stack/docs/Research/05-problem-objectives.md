# Vistara — Day 5: Problem & Objectives

> Track: Full Stack / Product | Phase 1 — Research & Scope | Day 5/90
> Locks the final problem statement and platform objectives from Day 1-4. Nothing new introduced.

## 1. Final Problem Statement

> **Accommodation discovery is mature and well-served by existing platforms. Trust is not. Guests have no reliable way to know what's actually been verified about a host or property, no clear record of what they agreed to before booking, no structured way to report when reality doesn't match the listing, and no easy way to judge review quality or price fairness. Vistara exists to make trust a visible, verifiable, structured part of the booking experience — not a backend afterthought.**

This directly answers all six Day 3 gaps and is confirmed by all seven Day 4 personas.

## 2. Platform Objectives

### Guest-facing objectives
- See verification status (property/photo-based, not ID-document — see Day 8 scope) directly on a listing before booking (Gap 1)
- See host requirements clearly and confirm them at booking, with a permanent record (Gap 2)
- Report mismatches between listing claims and actual experience through a dedicated flow, separate from a public review (Gap 3)
- Understand review quality through structured, aspect-based ratings, not just a star average (Gap 4)
- See a clear price breakdown before payment (Gap 5)
- Eventually see trust signals factored into ranked results, once the risk model exists (Gap 6, Phase 6-8)

### Host-facing objectives
- Build credibility through automated property/photo verification, independent of review volume
- Set clear requirements that guests must acknowledge before booking
- Have a recorded snapshot of agreed requirements to reference in disputes

### Admin-facing objectives
- Review flagged verification cases and mismatch reports through a structured queue, not raw submissions
- Approve, flag-for-review, or escalate cases with an audit trail

## 3. Objectives Explicitly Out of Scope

Unchanged from prior scope decisions:
- ID-document identity verification (explicit roadmap exclusion)
- Business/certificate verification
- Destination/"Explore" discovery, hidden gems, guide marketplace, trip planner, parking marketplace, local food discovery — logged in `Vistara-Major-Future-Roadmap.md`, pending an explicit decision to reopen

## 4. Success Definition for Phase 1

By Day 14, the team should answer without hesitation:
- What are we building, in one sentence? (Section 1)
- What does a guest get that they can't get elsewhere? (Verification visibility + requirement snapshot + mismatch reporting + structured reviews)
- What's explicitly not being built, and why? (Section 3, cross-referenced to the future-roadmap file)

## 5. Day 5 Conclusion

Problem and objectives are locked, consistent with the corrected Day 3 gap set and Day 4 personas. No further changes to "why Vistara exists" without explicitly reopening this document.

Next: Day 6 — Proposed solution, translating these objectives into platform modules.
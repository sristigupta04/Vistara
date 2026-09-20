# Vistara — Day 4: Users & Personas

> Track: Full Stack / Product | Phase 1 — Research & Scope | Day 4/90
> Personas test whether Day 3's six gaps are real problems for real people. No new features introduced here.

## Objective

Define who experiences the six Day 3 gaps concretely enough to design against: Guest, Host, Admin.

---

## Guest Personas

### Persona A — First-time solo traveller
Books unfamiliar cities alone, no personal network to vet listings. Primary fear: arriving to a property that doesn't match photos, with no one to call.
**Gaps:** 1 (Trust Visibility), 3 (Expectation vs. Experience)

### Persona B — Family booking for parents
Books on behalf of parents who won't complain in real time even if something's wrong. Needs certainty *before* booking, not recourse after.
**Gaps:** 1 (Trust Visibility), 2 (Requirement Clarity — pet/smoking/ID rules must be unambiguous upfront)

### Persona C — Repeat budget traveller
Books frequently, price-sensitive, compares many listings. Wants to know if a price is fair, not just cheap.
**Gaps:** 5 (Price Transparency), 4 (Review Understanding — to judge real value, not just star average)

### Persona D — Time-pressed planner
Wants to book quickly without opening 15 listings to compare. Would use AI-assisted search if it actually surfaced trustworthy options, not just cheap ones.
**Gaps:** 6 (Trust-Aware Discovery)

---

## Host Personas

### Persona E — New host, first property
No reviews yet, no way to signal legitimacy. Wants a path to build credibility independent of review volume.
**Gaps:** 1 (Trust Visibility — verification gives new hosts a signal beyond review count)

### Persona F — Experienced host, disputes with guests
Has had guests violate house rules and deny being told. Wants proof of what was agreed to at booking time.
**Gaps:** 2 (Requirement Clarity — requirement snapshot as a dispute record)

---

## Admin Persona

### Persona G — Platform trust/safety admin
Reviews flagged verification cases and mismatch reports. Needs well-organized cases to act efficiently, not raw text dumps.
**Gaps:** 1, 3 — everything that generates a reviewable case

---

## Persona → Gap Coverage Check

| Gap | Covered by |
|---|---|
| 1. Trust Visibility | A, B, E, G |
| 2. Requirement Clarity | B, F |
| 3. Expectation vs. Experience | A, G |
| 4. Review Understanding | C |
| 5. Price Transparency | C |
| 6. Trust-Aware Discovery | D |

Every gap has at least one persona depending on it. Gaps 1–3 (the core trust mechanics) have the strongest multi-persona pressure — confirming Day 3's implicit prioritization even though this pass didn't rank the gaps explicitly.

## What's Deliberately Not a Persona Here

No "group of friends," no "pilgrimage tour group," no "trip planner," no "local guide seeker." Those belong to the parked ideas in `Vistara-Major-Future-Roadmap.md`, not this scope.

## Day 4 Conclusion

> **Seven personas (4 guest, 2 host, 1 admin) map cleanly onto all six Day 3 gaps — no orphaned gap, no persona introducing scope beyond what's frozen.**

Next: Day 5 — Problem & Objectives.
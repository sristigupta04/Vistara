# Vistara — Day 3: Gap Analysis

> Scope note: Narrows Day 2's finding (trust is invisible everywhere) into specific, buildable gaps. No new ideas introduced here — only sharpening what Day 1 and Day 2 already established.

---

## 1. Day 3 Objective

Convert "trust is invisible" into 5–7 gaps specific enough to design against. A gap only qualifies if it's:
- Traceable to a problem named in Day 1
- Confirmed absent (or weak) across competitors in Day 2
- Buildable by a 2-person team without external dependencies that don't yet exist (e.g., no gap requiring a licensed verification API we haven't secured)

---

## 2. The 6 Confirmed Gaps

### Gap 1 — Verification is invisible to the guest
Competitors verify hosts/businesses on the backend, but the guest never sees *what* was checked. There's no listing-level trust display.

### Gap 2 — Reviews aren't tied to verified stays
Anyone can review; nothing distinguishes a review from an actual completed, verified booking. "Verified Stay" as a visible tag does not exist as standard practice.

### Gap 3 — No structured post-stay mismatch reporting
If a listing doesn't match reality, a guest's only options are a public review or a support ticket — no dedicated "claim vs. experience" reporting flow that feeds back into the platform's trust data.

### Gap 4 — Host requirements aren't confirmed or recorded at booking time
Guests may not see house rules/requirements clearly before paying, and there's no record of what was agreed to at the moment of booking (useful for disputes on both sides).

### Gap 5 — Price transparency is inconsistent
Fees often appear late in checkout; no easy way to gauge whether a price is reasonable for the category/location.

### Gap 6 — AI discovery isn't connected to trust
Where AI-assisted search/recommendation exists (Agoda, emerging elsewhere), it optimizes for price/preference match — never for trust signals as a ranking factor.

---

## 3. Gap Prioritization

| Gap | Directly buildable in MVP? | Core to thesis? |
|---|---|---|
| 1. Verification visibility | Yes | Yes — central |
| 2. Verified Stay reviews | Yes | Yes — central |
| 3. Mismatch reporting | Yes | Yes — central |
| 4. Requirement confirmation + snapshot | Yes | Yes — supporting |
| 5. Price transparency | Yes (basic breakdown only) | Secondary |
| 6. Trust-aware AI ranking | Partial (basic version only) | Secondary, Major-leaning |

Gaps 1–4 form the actual backbone of Vistara's MVP. Gaps 5–6 are real but smaller — basic versions belong in MVP, advanced versions belong later (Money Radar, trust-aware AI ranking).

---

## 4. What's Deliberately Left Out

Not every gap identified in earlier (now-superseded) research gets carried forward:

- **Regulatory compliance** — a real gap, but not a guest-facing trust gap; it's a legal/ops concern for later stage, not core differentiation.
- **Photo/image authenticity detection** — real gap, but requires ML capability not yet built; parked for Major.
- **Fraud/risk scoring** — same as above; the MVP handles this through admin review, not automated scoring.

These aren't rejected — they're sequenced correctly instead of front-loaded.

---

## 5. Day 3 Conclusion

> **Vistara's MVP has four core gaps to solve (verification visibility, verified reviews, mismatch reporting, requirement confirmation) and two supporting gaps to address at a basic level (price transparency, trust-aware discovery). Everything else is Major-phase or out of scope.**

Next: **Day 4 — Users & personas**, defining who actually experiences these six gaps (guest, host, admin) before designing solutions.
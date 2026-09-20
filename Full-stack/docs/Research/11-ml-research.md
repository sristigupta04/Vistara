# Vistara — Day 11: ML Research

> Fully corrected. The original version of this document claimed the MVP had exactly one AI feature (natural-language search) and deferred everything else to "Major." That was wrong and contradicted the project's own 90-Day Roadmap, which specifies four real ML components within the 90 days. This version replaces it entirely.

## 1. Objective

Choose realistic methods for each ML component the roadmap actually specifies, without over-scoping into research territory the team can't execute in the available time.

## 2. The Four In-Scope ML Components

| Component | Phase | Problem | Realistic Method |
|---|---|---|---|
| Recommendation | 5 (Days 43-49) | Rank properties by relevance to a user | Content-based baseline (attribute similarity); incorporate interaction data (USER_EVENT) as it accumulates |
| Trust/risk scoring | 6 (Days 50-56) | Flag properties/hosts needing review | Baseline classifier (logistic regression or similar) on booking/mismatch/verification signals |
| Review intelligence | 7 (Days 57-60) | Summarize review sentiment by aspect | Aspect-based sentiment extraction mapped to existing sub-rating categories (cleanliness, accuracy, communication, value) |
| Photo/property verification | 7 (Days 61-66) | Detect duplicate/inconsistent property images | Perceptual hashing + similarity scoring |

None of these require novel research — all are well-established, realistic methods for a 2-person team on this timeline, which is exactly why the roadmap scheduled them where it did.

## 3. Natural-Language Search — Correctly Scoped as Secondary

This is the one MVP-era AI convenience feature, and it remains small deliberately: an LLM API call converting free text into structured search parameters, with mandatory fallback to manual filters (per NFR-AI-06). It belongs in Phase 8 (Day 71) alongside personalization work, not as MVP's only AI feature — the earlier version of this document was wrong to treat it as such.

## 4. Why Not More Than These Four

Being honest about limits: none of these four components require deep learning, large training datasets, or infrastructure beyond a single FastAPI service. Going further (e.g., building a custom embedding model, real-time fraud detection, or generative review summarization) would exceed both the timeline and the available data volume from a 30-50 property seed dataset. The roadmap's own scope is already appropriately ambitious without stretching into research the team can't validate in 90 days.

## 5. Data Sufficiency Check

With a seed dataset of 30-50 properties and no real user history at Phase 5's start:
- **Recommendation:** content-based works fine with attribute data alone; collaborative/interaction-based components genuinely need usage data, which won't exist yet — Phase 8 personalization is correctly positioned *after* enough Phase 3-4 platform usage (even just team/tester usage) generates USER_EVENT data.
- **Risk classifier:** will have very few real positive examples (genuine risk cases) at this scale — Day 20 already accounts for this by treating admin decisions as ongoing training labels rather than expecting a fully trained model by Day 56.
- **Review intelligence and photo verification:** don't require large datasets to produce reasonable baseline results, since they're per-item analyses, not population-level models.

## 6. Day 11 Conclusion

> **Four ML components, each with a realistic, achievable method for a 2-person team, each correctly phased against when the data needed for it actually exists. This replaces the earlier, incorrect single-AI-feature framing.**

Next: Day 12 — Dataset strategy (see correction to verification-API wording).
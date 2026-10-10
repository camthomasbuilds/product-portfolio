# Framework: AI Architecture Patterns for Industrial Products

## Overview

These are reusable technical architecture patterns I've applied across four AI/ML product lines in power generation. Each pattern emerged from shipping real products in high-stakes, regulated environments, not from theory. They prioritize trust, explainability, and graceful degradation over novelty.

---

## Pattern 1: Specialized Agents Over General-Purpose Models

**The pattern:** When building AI systems that must handle multiple distinct categories or document types, build specialized models/agents instead of one general-purpose system.

**Where I applied it:**
- **DocIQ:** Three specialized extraction agents (drawings, records, manuals) instead of one universal document processor. Each agent is tuned to its document type's field structure, vocabulary, and layout patterns.
- **GenE:** Per-inverter power surface models (10,000+ individual models) instead of fleet-wide or site-wide models. Each inverter has unique characteristics.
- **Nuclear:** Per-system monitoring models tuned to specific equipment physics, not a generic anomaly detector.

**Why it works:**
- Specialized models outperform general ones by 10-20% in every case I've tested
- Error analysis is actionable ("the drawings agent struggles with I&C loop diagrams") vs. vague ("the model is 80% accurate")
- You can improve one agent without risking regressions in others
- Resource allocation is precise: invest in the worst-performing agent, not the whole system

**When NOT to use it:**
- Volume per category is too low to train specialized models
- Categories share so much structure that specialization adds complexity without accuracy gains
- You need to handle novel categories at runtime (specialization can't handle the unknown)

**The tradeoff:** More models to maintain. Mitigate with shared training infrastructure and standardized evaluation frameworks.

---

## Pattern 2: Confidence-Gated Automation

**The pattern:** Every AI prediction includes a continuous confidence score (0-1). Confidence determines the automation level: high → auto-execute, medium → route to review, low → flag for expert or reject.

```
Prediction + Confidence Score
     │
     ├── ≥ 0.90  →  Auto-execute (no human touch)
     ├── 0.70-0.89 →  Route to review queue
     └── < 0.70   →  Flag for expert / reject
```

**Where I applied it:**
- **DocIQ:** High-confidence classifications auto-file to the content management system. Uncertain ones queue for review. Admin-adjustable thresholds per field and pipeline.
- **GenE:** Loss classifications with high confidence are finalized automatically. Ambiguous intervals (e.g., overlapping curtailment + fault) are flagged for analyst review in DTE.
- **Nuclear:** Alert confidence determines triage priority. High-confidence alerts with agreement between physics-based and statistical models route directly to work-order creation.

**Critical implementation details:**
- Thresholds are **product decisions**, not model decisions. The PM owns where to draw the line.
- Thresholds must be adjustable **without code deploys** (config, admin UI, or environment variable).
- Monitor **boundary accuracy**: items near the threshold are where errors concentrate.
- Track **automation error rate** (sampled human audit of auto-executed items) and **review override rate** (how often reviewers agree with the model).

**The tradeoff:** Conservative thresholds mean more human review (higher cost, slower throughput). Aggressive thresholds mean more automation errors (trust erosion, compliance risk). Start conservative. Tighten as you build evidence.

---

## Pattern 3: Phased Trust Architecture

**The pattern:** Don't go from "no AI system" to "automated decisions" in one step. Build trust incrementally through four phases, with explicit gates between each.

| Phase | System Does | User Does | Gate to Next Phase |
|-------|-----------|----------|-------------------|
| 1. Read | Displays data accurately | Validates data quality | Data quality metrics meet threshold |
| 2. Detect | Surfaces anomalies and alerts | Investigates and confirms/dismisses | Alert precision meets threshold |
| 3. Recommend | Suggests actions with reasoning | Decides whether to act | Recommendation acceptance rate |
| 4. Act | Executes low-risk decisions automatically | Reviews automated decisions | Automation error rate below threshold |

**Where I applied it:**
- **Nuclear:** Phase 1 (data display) → Phase 2 (alert review) → Phase 3 (work-order recommendations) → Phase 4 (automated work-order creation for confirmed patterns)
- **DocIQ:** Phase 1 (classification display) → Phase 2 (confidence scoring) → Phase 3 (auto-file high confidence) → Phase 4 (forward-fill live processing)
- **GenE:** Phase 1 (generation data) → Phase 2 (loss classification) → Phase 3 (month-end recommendations) → Phase 4 (auto-rules for known patterns)

**Why it works in regulated/high-stakes environments:**
- Operators see the system prove itself before they're asked to trust it
- Each phase has measurable success criteria, not subjective buy-in
- Failure at any phase is contained. You roll back one phase, not the whole system
- Regulators and auditors can trace the trust-building evidence

**The tradeoff:** Slower time to full automation. But in nuclear and financial reporting, rushing to Phase 4 and having a false alarm erode operator trust costs you 6+ months of re-earned credibility. The phased approach is faster in the long run.

---

## Pattern 4: Financial Anchoring

**The pattern:** Every technical finding, alert, or classification connects to a dollar value. Don't surface "anomaly detected": surface "this anomaly represents $X in risk."

**Where I applied it:**
- **GenE:** Loss classifications map to financial cost centers. "This site lost 450 MWh to subcurve underperformance" becomes "$67K in recoverable generation this month."
- **Fossil:** Weibull failure predictions connect to Total Value framework. "30% failure probability" becomes "30% chance of a $2.4M event in 12 months."
- **Nuclear:** Degradation alerts connect to forced outage cost. "Pump vibration trending above baseline" becomes "early indicator for a potential $3M/day forced outage event."
- **DocIQ:** Misclassification connects to search time cost. "This document type has 72% accuracy" becomes "$420K/yr in wasted search time for this category."

**Why it works:**
- Converts technical findings into capital allocation decisions
- Enables risk-weighted prioritization (which alerts to act on first)
- Makes the business case self-evident: users see the dollar value of the system every time they use it
- Aligns technical teams and business stakeholders on the same metric

**The tradeoff:** Requires maintaining a financial model alongside the technical system. The dollar values are estimates, not precise calculations. Be transparent about confidence ranges.

---

## Pattern 5: Performance as Product Architecture

**The pattern:** Treat query performance as a first-class architectural decision, not an optimization to do later. In data-heavy products, response time determines adoption patterns.

| Response Time | User Behavior | Product Implication |
|--------------|--------------|-------------------|
| < 300ms | Interactive exploration, ad-hoc analysis | Users discover insights they wouldn't have looked for |
| 1-3 seconds | Tolerable for planned queries | Users do what they came to do and leave |
| 3-10 seconds | Frustration, tab-switching | Users return to spreadsheets |
| > 10 seconds | Abandonment | Product fails regardless of feature quality |

**Where I applied it:**
- **GenE:** Drove the Python/FastAPI → Rust/Axum migration specifically because 3-5s response times were killing adoption. Sub-300ms enabled usage patterns (ad-hoc fleet exploration, real-time comparisons) that changed how operations teams worked.
- **GenE DB:** TimescaleDB with continuous aggregates at 5 rollup tiers (1m, 5m, 10m, 1h, daily). Pre-computing aggregates trades storage for query speed.

**Architectural implications:**
- Choose languages/frameworks based on production query patterns, not developer productivity alone
- Pre-compute aggregations at write time rather than calculating at read time
- Profile real user queries, not synthetic benchmarks
- Monitor P95 latency, not averages: the worst experiences drive abandonment

**The tradeoff:** Rust is harder to hire for and slower to develop in than Python. TimescaleDB continuous aggregates increase storage costs and write complexity. These are worth it when the product's adoption depends on interactive performance.

---

## Pattern 6: Graceful Degradation

**The pattern:** When any component fails: model confidence drops, data source goes offline, API times out: the system defaults to a safe, useful state rather than breaking or producing bad output.

**Degradation hierarchy:**
1. **Full automation** (everything working) → system operates normally
2. **Reduced automation** (model confidence low) → route to human review, continue processing
3. **Reduced features** (data source offline) → show available data with "source unavailable" indicator, don't show stale data as current
4. **Manual fallback** (system down) → users can perform critical workflows manually with data exports

**Where I applied it:**
- **DocIQ:** When classifier confidence drops, documents queue for review rather than being misclassified
- **GenE:** When GenE classification fails for an interval, it's marked Invalid and implied power fills the gap: visible to analysts, not hidden
- **Nuclear:** When data historian connectivity is inconsistent, Conduit shows last-known data with freshness timestamps rather than hiding the gap

**Why it matters in industrial settings:** Power plant operators make safety and financial decisions based on these systems. Silent failure, where the system looks normal but the data is wrong, is the worst possible outcome. Visible degradation is always safer than hidden failure.

---

## Choosing Patterns by Context

| Context | Primary Patterns |
|---------|-----------------|
| **Regulated environment** (nuclear, financial) | Phased Trust + Confidence Gating + Graceful Degradation |
| **High data volume** (fleet telemetry, document processing) | Specialized Agents + Performance Architecture |
| **Capital allocation decisions** | Financial Anchoring + Confidence Gating |
| **Skeptical user base** | Phased Trust + Performance Architecture + Human-in-the-Loop |
| **Multi-product portfolio** | All patterns standardized across products for consistency and reuse |

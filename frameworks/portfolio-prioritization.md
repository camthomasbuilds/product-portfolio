# Framework: Portfolio Prioritization for Multi-Product PMs

## The Problem

When you own one product, prioritization is hard. When you own four independent products — each with different stakeholders, different value models, and different risk profiles — prioritization becomes a portfolio management problem.

The question isn't "should we build Feature X?" It's "should we invest our next dollar of engineering capacity in Product A's Feature X, Product B's Feature Y, or Product C's infrastructure work that unblocks three downstream initiatives?"

This framework is how I make those decisions.

---

## The Framework: Risk-Adjusted Value Allocation

### Step 1: Quantify Every Initiative

Every initiative — regardless of which product it belongs to — gets the same evaluation:

| Field | What It Answers |
|-------|----------------|
| **NPV** | What's the net present value over 3-5 years? |
| **Annual value** | What's the steady-state annual benefit once shipped? |
| **Investment cost** | Engineering quarters, infrastructure spend, opportunity cost |
| **Profit Index** | NPV / Investment cost. Higher = better return per dollar. |
| **Time to value** | How many quarters until first dollar of return? |
| **Confidence level** | How certain are we about the value estimate? (High/Med/Low) |

This creates a common currency across products. A nuclear monitoring feature and a solar curtailment improvement can be directly compared.

### Step 2: Apply Strategic Multipliers

Raw financial value isn't enough. Some initiatives have strategic value that the NPV doesn't capture:

| Multiplier | When to Apply | Example |
|-----------|---------------|---------|
| **Platform leverage** (1.5x) | Creates reusable capability for other products | Itasca telemetry serves GenE AND Nuclear |
| **Blocking dependency** (2x) | Other high-value work is gated on this | PI integration blocking all Nuclear features |
| **Regulatory deadline** (2x) | Non-delivery creates compliance exposure | SOX reporting requirements |
| **Commercialization enabler** (1.5x) | Required for external product/revenue | GenE SaaS readiness features |
| **Trust-building** (1.3x) | Builds stakeholder confidence enabling larger investments later | Nuclear pilot success gates full deployment |

### Step 3: Penalize for Risk

Adjust the value downward based on execution risk:

| Risk Factor | Penalty |
|------------|---------|
| **Data not ready** | 0.7x (30% haircut) |
| **Team unfamiliar with domain** | 0.8x |
| **External dependency (IT, vendor, API)** | 0.7x |
| **Unclear ownership** | 0.6x |
| **Novel technology (unproven at our scale)** | 0.8x |

### Step 4: Stack-Rank and Draw the Line

After adjustments, the formula is:

```
Adjusted Value = (NPV × Strategic Multiplier × Risk Penalty) / Investment Cost
```

Stack-rank all initiatives across the portfolio by Adjusted Value. Draw a line at available engineering capacity. Everything above the line gets funded. Everything below gets a "not now" with a clear explanation of why.

---

## Real Example: Q2 2026 Portfolio Allocation

| Initiative | Product | Raw NPV | Multiplier | Risk | Adjusted Score | Decision |
|-----------|---------|---------|-----------|------|---------------|----------|
| Degradation/Soiling Bifurcation | GenE | $21M | 1.0x | 0.9 | 81.2 | **Fund** |
| Wind Curtailment Classification | GenE | $8.5M | 1.0x | 0.9 | 25.8 | **Fund** |
| Solar Fleet Standardization | GenE | $25.8M (3yr) | 1.3x | 0.8 | 22.1 | **Fund** |
| PI Integration Stabilization | Nuclear | N/A | 2.0x (blocker) | 0.7 | High | **Fund** (unblocks N1-N5) |
| DocIQ Phase 2 Production | DocIQ | $3.8M/yr | 1.5x (platform) | 0.8 | 14.2 | **Fund** |
| Fossil Weibull Expansion | Fossil | Part of $20M | 1.0x | 0.7 | 11.8 | **Fund** |
| GCP Full Migration | GenE | $1.7M | 1.5x (platform) | 0.7 | 6.1 | **Fund (phased)** |
| Economic Curtailment Split | GenE | Low | 1.0x | 0.9 | 2.1 | **Defer** — BI tool scope |
| General-purpose doc classifier | DocIQ | Low | 1.0x | 0.8 | 1.4 | **Kill** — specialized agents won |

---

## How I Communicate Prioritization Decisions

### To Engineering Teams
"Here's what we're building this quarter and why. Here's what we're not building and why. The ranking is based on [specific values]. If you think I'm wrong about an assumption, challenge me — I'd rather be corrected now than discover it at sprint review."

### To Stakeholders Whose Initiative Got Deferred
"Your initiative has a [specific value]. It's ranked [Nth] in the portfolio. The initiatives ahead of it have higher adjusted value because [specific reasons]. Here's what would need to change for it to move up: [data readiness, dependency resolution, etc.]. I'm not saying no — I'm saying not yet, and here's the path to yes."

### To Leadership
"The portfolio is allocating $X in engineering capacity across [N] initiatives with a combined expected value of $Y. Our top initiative has an 81.2 profit index — $81 in value for every $1 invested. The lowest-ranked funded initiative has a [Z] profit index. Here's the 'below the line' list and what we'd need to fund them."

---

## Anti-Patterns

| Anti-Pattern | Why It Fails | What to Do Instead |
|-------------|-------------|-------------------|
| **Equal allocation across products** | Treats all products as equally valuable regardless of actual returns | Allocate by adjusted value, even if it means one product gets zero this quarter |
| **Loudest stakeholder wins** | Rewards political skill, not business value | Quantify everything; show the math |
| **Sunk cost priority** | "We already started X" biases toward completion over value | Evaluate remaining value vs. remaining cost, not total invested |
| **Ignoring platform work** | Unglamorous infrastructure work that unblocks 3 products loses to a flashy feature | Strategic multipliers make platform leverage visible |
| **Single-quarter horizon** | Over-indexes on quick wins, under-invests in compounding value | NPV forces multi-year thinking |

---

## When This Framework Breaks

- **Crisis response** — When a production system is down or a regulatory deadline is imminent, skip the framework and fix the problem. Recalibrate later.
- **Strategic bets** — Some investments can't be NPV'd (e.g., exploring a new market). Keep a small allocation (10-15%) for strategic bets evaluated on learning value, not financial return.
- **Team health** — If a team has shipped 3 high-pressure quarters in a row, the right investment might be a lower-pressure initiative that prevents burnout. The framework doesn't capture human factors.

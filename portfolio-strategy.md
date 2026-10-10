# Portfolio Strategy: Enterprise AI for Power Generation

## The Investment Thesis

Every generation asset — solar, wind, gas, nuclear — produces data continuously. That data is currently trapped in fragmented systems, processed manually, and acted on reactively. The thesis: **structure that data correctly, and it becomes a decision-making system that replaces millions of dollars in manual work, prevents millions more in unplanned outages, and creates an entirely new class of operational intelligence.**

I'm building that system across four product lines. Not as one monolithic platform, but as a portfolio of specialized products that share architecture patterns, feed each other data, and compound in value.

---

## Portfolio Architecture

```
              ┌─────────────────────────────────────────────────┐
              │              GENERATION FLEET                     │
              │   700+ Solar/Wind  │  10+ Fossil  │  2 Nuclear   │
              └────────┬───────────┴──────┬───────┴──────┬───────┘
                       │                  │              │
                       ▼                  ▼              ▼
              ┌────────────────┐  ┌──────────────┐  ┌──────────────┐
              │     GenE       │  │   Fossil AH   │  │  Nuclear AH  │
              │ Classification │  │   Weibull +    │  │  Physics +   │
              │ + OpsReport    │  │  Total Value   │  │  Statistical │
              └───────┬────────┘  └──────┬────────┘  └──────┬──────┘
                      │                  │                   │
                      ▼                  ▼                   ▼
              ┌─────────────────────────────────────────────────┐
              │                    Conduit                       │
              │     Unified Asset Intelligence Platform          │
              │   Asset pages + Alerts + Work orders + Docs      │
              └────────────────────────┬────────────────────────┘
                                       │
                                       ▼
              ┌─────────────────────────────────────────────────┐
              │                    DocIQ                         │
              │    Document Classification + Metadata            │
              │    650K docs → Searchable + Governed             │
              └─────────────────────────────────────────────────┘
```

### How the Products Connect

| From | To | What Flows |
|------|-----|-----------|
| GenE (Itasca telemetry) | Nuclear Nexus | Shared telemetry backbone — built once, serves both |
| DocIQ | Conduit asset pages | Classified documents linked to equipment for operator access |
| Nuclear/Fossil models | Conduit alerts | Predictive alerts surface in unified triage workflow |
| GenE classifications | Financial systems | Loss categories → cost centers → revenue recognition |
| DocIQ confidence pattern | Nuclear + Fossil products | Confidence-gating architecture reused across product lines |
| GenE Rust/TimescaleDB | Adjacent teams | Architecture pattern adopted as reference for 3+ teams |

---

## Investment Framework

Every initiative across the portfolio competes for allocation using the same framework:

### How I Evaluate

| Factor | Weight | What I Measure |
|--------|--------|---------------|
| **Financial value** | 40% | NPV, annual savings, revenue protected/recovered |
| **Strategic dependency** | 25% | Does this unblock other products? Does it create reusable capability? |
| **Data readiness** | 15% | Do we have the data? Is it clean enough? What's the integration cost? |
| **Execution risk** | 10% | Team capacity, technical complexity, dependency chain length |
| **Time to value** | 10% | How quickly does the investment start paying back? |

### Current Portfolio Allocation

| Product | Active Charters | Combined Value | Profit Index Range |
|---------|----------------|----------------|--------------------|
| GenE | 4 workstreams | $55M+ NPV | 25.8 – 81.2 |
| DocIQ | 6 EPICs (Phase 2) | $3.8M+ net annual | 6.6x multiplier |
| Nuclear | 5 capability tracks (N1-N5) | $20M+ program | Outage prevention ($3M/day) |
| Fossil | 3 workstreams | $20M+ program | Integrated with Total Value |

### What I Chose NOT to Build (and Why)

The decisions to not build are as important as the decisions to build:

- **Did not build economic/non-economic curtailment analysis into GenE** — belongs in BI tools, not the classification engine. Keeping GenE focused on accuracy preserved the $8.5M NPV timeline.
- **Did not pursue deep learning for fossil failure prediction** — Weibull is interpretable, works with limited data, and is trusted by reliability engineers. Technical sophistication wasn't the bottleneck; stakeholder trust was.
- **Did not ship nuclear features in Q3 2026** — advocated for stabilization quarter instead. PI integration was 60-70% complete, ownership was unclear. Foundation work first.
- **Deferred WIT reclassification to DocIQ Phase 3** — the accuracy improvement wasn't worth the Phase 2 timeline risk. Shipped what mattered, deferred what could wait.
- **Did not build a general-purpose document classifier** — split into three specialized agents (drawings, records, manuals). Each outperformed the general model by 15%+.
- **Did not auto-categorize DTE events** — human-in-the-loop required for financial close integrity. The cost of an automated wrong answer exceeds the cost of a human review step.

---

## Cross-Product Architecture Principles

These are the patterns I established that now operate as standards:

### 1. Specialized Agents > General-Purpose Models
Proven across DocIQ (3 document agents), GenE (per-inverter power surfaces), and Nuclear (per-system monitoring). In every case, specialization outperformed generalization by 10-20%.

### 2. Confidence Gating
Every AI prediction includes a confidence score. High confidence → automate. Low confidence → human review. The threshold is a product decision, not a model decision. Adjustable without code deploys. Applied across DocIQ, GenE anomaly detection, and being adopted for Nuclear alert triage.

### 3. Human-in-the-Loop by Default
In regulated, financial, and safety-critical domains: automate the obvious, review the uncertain, never fail silently. Applied universally across the portfolio.

### 4. Phased Trust-Building
Don't go from "no system" to "automated decisions" in one step.
- Phase 1: Show data accurately (prove you can read)
- Phase 2: Surface insights (prove you can detect)
- Phase 3: Recommend actions (prove you can think)
- Phase 4: Automate low-risk decisions (prove you can act)
Applied in Nuclear (alert → triage → work order) and DocIQ (classify → review → auto-file).

### 5. Financial Connection
Every technical finding connects to a dollar value. GenE losses map to financial cost centers. Fossil failures connect to Total Value. Nuclear alerts connect to outage cost. This is what turns "interesting data" into "capital allocation decisions."

### 6. Performance is a Product Feature
If the system is too slow, users go back to spreadsheets (GenE Python backend) or manual processes. The Rust migration wasn't optimization — it was a product decision that changed adoption patterns. Sub-300ms response times enabled usage patterns that 3-5s response times made impossible.

---

## Portfolio Evolution

### Phase 1: Foundation (2024-2025)
- GenE v1 shipped, proving the classification engine concept
- DocIQ Phase 1 delivered, establishing the AI document pipeline
- Nuclear and Fossil discovery + initial pilots

### Phase 2: Scale (2025-2026)
- GenE v2 (Rust rewrite, 700+ sites, $55M+ NPV)
- DocIQ Phase 2 (production pipeline, forward-fill, ROT governance)
- Nuclear Q4 PRD (N1-N5 capability tracks)
- Fossil Weibull models (40%+ fleet coverage)

### Phase 3: Platform (2026-2027)
- GCP migration unifying telemetry backbone
- Conduit as cross-BU asset intelligence hub
- SaaS commercialization of GenE
- Quest maturity enabling closed-loop model improvement
- Full plant standard work orders (Nuclear capstone)
- Control loop performance monitoring (Fossil capstone)

### Phase 4: Business Model (2027+)
- GenE external SaaS for third-party asset owners
- Platform licensing revenue stream
- Portfolio becomes a product line with its own P&L

---

## The Principal PM Argument

This portfolio demonstrates Principal/Director-level product leadership:

| Dimension | Evidence |
|-----------|---------|
| **Portfolio scope** | 4 independent products, different teams, different domains, unified thesis |
| **Business model innovation** | SaaS commercialization — creating a new revenue line, not just shipping features |
| **Investment framework** | NPV-driven prioritization across $95M+ in combined portfolio value |
| **Architecture influence** | Patterns I designed (Rust/TSDB, multi-agent AI, confidence gating) adopted by 3+ adjacent teams |
| **Org-level impact** | Changed how the organization evaluates AI investments, plans quarters, and measures product value |
| **Regulated complexity** | NRC (nuclear), SOX/NERC (financial), engineering compliance — simultaneously |
| **Company-scale metrics** | $2.4B revenue influenced, $90M+ recovered, 700+ sites, 15GW |

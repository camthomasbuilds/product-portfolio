# Product Portfolio | Enterprise AI for Power Generation

## Investment Thesis

A Fortune 200 energy company operates 700+ renewable sites, 10+ fossil plants, and 2 nuclear stations generating $2.4B+ in annual revenue. The operational data from these assets is trapped in fragmented systems, processed manually, and acted on reactively.

**The opportunity:** Structure that data into decision-making systems and unlock $110M+ in value through recovered revenue, avoided outages, productivity gains, and new business models.

I own four product lines executing against this thesis.

---

## Portfolio Summary

| Product | Business Problem | Investment | Return |
|---------|-----------------|------------|--------|
| [GenE / OpsReport](https://github.com/camthomasbuilds/renewable-fleet-ops) | No system of record for $2.4B in generation revenue | Rust/TimescaleDB platform, 10K+ ML models | $55M+ NPV, $90M+ annual value |
| [DocIQ](https://github.com/camthomasbuilds/document-ai-pipeline) | 650K engineering docs with broken metadata | 3 specialized AI agents, confidence-gated pipeline | $3.4M/yr savings, 6.6x ROI |
| [Nuclear Asset Health](https://github.com/camthomasbuilds/nuclear-monitoring) | Manual monitoring, $3M/day forced outage exposure | Physics + statistical hybrid platform | 80% cost reduction, 6→30+ systems |
| [Fossil Asset Health](https://github.com/camthomasbuilds/predictive-asset-health) | Calendar-based maintenance, capital misallocation | Weibull failure models + financial integration | 70%+ coverage, $20M+ program |

These are four independent products with different teams, stakeholders, technology stacks, and regulatory requirements, unified by a shared investment thesis and allocation framework.

---

## How the Products Connect

```
GenE (data foundation)      →  Operational data for 700+ renewable sites
DocIQ (knowledge layer)     →  650K engineering documents, structured and governed
Nuclear (predictive layer)  →  Equipment degradation detected before $3M/day outages
Fossil (financial layer)    →  Failure predictions connected to capital allocation
```

The portfolio compounds. GenE's telemetry backbone now serves Nuclear. DocIQ's classified documents feed into the asset intelligence platform. The confidence-gating pattern I designed for DocIQ has been adopted by two additional product lines. The Rust/TimescaleDB architecture from GenE became the reference pattern for adjacent teams.

**Full strategy and architecture:** [`portfolio-strategy.md`](./portfolio-strategy.md)

---

## Capital Allocation Decisions

The decisions that define this portfolio are not what I built, but where I chose to invest and what I chose to kill.

**Funded:**
- Rust backend migration for GenE. Not a technical optimization. A product decision. Sub-300ms response times changed adoption patterns from 30 to 300+ DAU.
- SaaS commercialization of GenE. Identified that an internal platform could become an external revenue line. Built the business case for a Fortune 200 company to enter a new market.
- Multi-agent AI for DocIQ. Three specialized classifiers instead of one general model. 15%+ accuracy improvement across all categories.
- Stabilization quarter for Nuclear. Advocated for pausing feature delivery to fix foundations. Unpopular. Correct. Enabled Q4 execution.

**Killed or deferred:**
- Economic/non-economic curtailment analysis. BI tool scope, not classification engine scope. Preserved the $8.5M NPV timeline.
- Deep learning for fossil failure prediction. Weibull is interpretable, works with sparse data, and is trusted by reliability engineers. Stakeholder adoption, not model sophistication, was the bottleneck.
- General-purpose document classifier. Specialized agents won on performance and maintainability.
- Auto-categorization of DTE events. Human-in-the-loop required for financial close integrity.

---

## Case Studies

| Case Study | Strategic Question |
|-----------|-------------------|
| [Renewable Fleet Ops](https://github.com/camthomasbuilds/renewable-fleet-ops) | How do you build a system of record for $2.4B in revenue from scratch? |
| [Document AI Pipeline](https://github.com/camthomasbuilds/document-ai-pipeline) | When should AI automate and when should humans decide? |
| [Predictive Asset Health](https://github.com/camthomasbuilds/predictive-asset-health) | How do you connect engineering predictions to capital allocation? |
| [Nuclear Monitoring](https://github.com/camthomasbuilds/nuclear-monitoring) | How do you build trust in AI in a regulated, zero-failure environment? |
| [SaaS Commercialization](https://github.com/camthomasbuilds/saas-commercialization) | How do you turn an internal tool into an external business? |

---

## Frameworks

Reusable decision-making models I've developed and applied across the portfolio:

| Framework | Core Question It Answers |
|-----------|------------------------|
| [Portfolio Prioritization](./frameworks/portfolio-prioritization.md) | Where should the next dollar of engineering capacity go? |
| [Enterprise GTM Playbook](./frameworks/enterprise-gtm-playbook.md) | How do you drive adoption when users didn't choose your product? |
| [AI Architecture Patterns](./frameworks/ai-architecture-patterns.md) | What technical patterns work when AI meets regulated industry? |
| [ML Product Lifecycle](./frameworks/ml-product-lifecycle.md) | How do you manage a product where "done" doesn't exist? |
| [Confidence Threshold Design](./frameworks/confidence-threshold-design.md) | How do you decide what to automate vs. what needs human judgment? |

---

## Portfolio Metrics

| Category | Metric |
|----------|--------|
| **Total portfolio value** | $110M+ (NPV + annual savings + program value) |
| **Revenue influenced** | $2.4B annual generation revenue |
| **AI at scale** | 10,000+ ML models in production, 3 AI classifiers, 6+ predictive models |
| **Data infrastructure** | 900M+ time-series records, 80GB/day ingestion |
| **User adoption** | 300+ DAU through product-led growth, zero mandates |
| **Capital efficiency** | Profit indices from 25.8 to 81.2 across active charters |
| **Regulatory scope** | NRC (nuclear), SOX/NERC (financial), engineering compliance |

---

## The Principal PM Case

| Dimension | Evidence |
|-----------|---------|
| **Portfolio ownership** | Four independent products, four P&Ls, one investment framework |
| **Business model creation** | SaaS commercialization: new revenue line for a Fortune 200 company |
| **Capital allocation** | NPV-driven prioritization across $110M+ in combined portfolio value |
| **Organizational influence** | Architecture patterns adopted by 3+ adjacent teams. Changed how the org evaluates AI investments. |
| **Regulated complexity** | NRC, SOX/NERC, engineering compliance, simultaneously |
| **Company-scale impact** | $2.4B revenue influenced, 700+ sites, 15GW fleet |

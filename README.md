# Product Portfolio | Energy & AI

I lead a portfolio of four AI and data platform products at a Fortune 200 energy company. Together, they form a connected intelligence layer across the entire generation fleet — renewable, fossil, and nuclear — driving $90M+ in recovered value, $20M+ in predictive maintenance value, and $3.4M in productivity savings annually.

**My thesis:** Every generation asset produces data that, when structured correctly, becomes a decision-making system. I'm building that system across four domains.

---

## The Portfolio

| Product | Domain | Scale | Value |
|---------|--------|-------|-------|
| [GenE / OpsReport](https://github.com/camthomasbuilds/renewable-fleet-ops) | Renewable fleet operations | 700+ sites, 15GW, $2.4B revenue influenced | $55M+ NPV, $90M+ annual value |
| [DocIQ](https://github.com/camthomasbuilds/document-ai-pipeline) | Document intelligence | 650K documents, 3 AI classifiers | $3.4M/yr savings, 6.6x ROI |
| [Nuclear Asset Health](https://github.com/camthomasbuilds/nuclear-monitoring) | Nuclear predictive monitoring | 2 nuclear stations, 30+ systems roadmap | 80% cost reduction, $3M/day outage prevention |
| [Fossil Asset Health](https://github.com/camthomasbuilds/predictive-asset-health) | Fossil predictive maintenance | 10+ gas generation sites | 70%+ component coverage, $20M+ program value |

These are not four features in one product. They are **four independent products** — different teams, different stakeholders, different technology stacks, different regulatory environments — unified by a shared investment thesis and architecture philosophy.

---

## Portfolio Strategy

The products are sequenced and connected:

```
GenE (data foundation)      →  Captures operational data for 700+ renewable sites
DocIQ (knowledge layer)     →  Structures 650K engineering documents for searchability
Nuclear (predictive layer)  →  Detects equipment degradation before $3M/day outages
Fossil (financial layer)    →  Connects failure predictions to capital allocation decisions
```

Each product creates data and capabilities that the others consume. GenE's telemetry backbone (Itasca) now serves Nuclear Nexus. DocIQ's classified documents feed into Conduit's asset pages. The confidence-gating pattern I designed for DocIQ is being adopted by two additional product lines. The Rust/TimescaleDB architecture I drove for GenE became the reference pattern for adjacent teams.

**Read the full strategy:** [`portfolio-strategy.md`](./portfolio-strategy.md)

---

## What I Actually Do

I don't just ship features. I make the decisions that determine which products get built, how they connect, and where the organization invests.

**Investment decisions I've made:**
- Chose Weibull over deep learning for fossil failure prediction (interpretability + data scarcity > technical sophistication)
- Drove the Python-to-Rust backend migration for GenE (product decision, not technical — sub-300ms response times changed adoption patterns)
- Said no to economic/non-economic curtailment splitting in GenE (kept the product focused on classification accuracy, let BI tools handle financial analysis)
- Advocated for a nuclear stabilization quarter instead of shipping features (unpopular but correct — foundation work made Q4 execution possible)
- Designed the multi-agent architecture for DocIQ instead of one general-purpose model (specialized agents outperformed by 15%+ across all categories)
- Built the business case for GenE SaaS commercialization (new revenue line for a Fortune 200 company)

**Organizational patterns I established:**
- Confidence-threshold gating pattern — now adopted across 3 product lines
- ROI-driven charter framework — every initiative competes with quantified NPV and profit index
- Phased trust-building deployment — pilot → validate → scale, with Go/No-Go gates
- Human-in-the-loop by default — automate high-confidence, route uncertain to review, never fail silently

---

## Case Studies

| Case Study | What It Demonstrates |
|-----------|---------------------|
| [`renewable-fleet-ops`](https://github.com/camthomasbuilds/renewable-fleet-ops) | 0-to-1 platform creation, architecture decisions, GTM strategy, 30→300+ DAU |
| [`document-ai-pipeline`](https://github.com/camthomasbuilds/document-ai-pipeline) | AI product management, confidence gating, human-in-the-loop design |
| [`predictive-asset-health`](https://github.com/camthomasbuilds/predictive-asset-health) | Technical tradeoff decisions (Weibull vs ML), financial framework integration |
| [`nuclear-monitoring`](https://github.com/camthomasbuilds/nuclear-monitoring) | Regulated environment, trust engineering, vendor-to-platform migration |
| [`saas-commercialization`](https://github.com/camthomasbuilds/saas-commercialization) | Business model innovation — internal tool to external SaaS product |

---

## Frameworks

Reusable patterns I've developed and applied across products:

| Framework | What It Covers |
|-----------|---------------|
| [`portfolio-prioritization.md`](./frameworks/portfolio-prioritization.md) | How I evaluate, rank, and allocate across a multi-product portfolio |
| [`enterprise-gtm-playbook.md`](./frameworks/enterprise-gtm-playbook.md) | How to get enterprise users to actually adopt internal products |
| [`ai-architecture-patterns.md`](./frameworks/ai-architecture-patterns.md) | Technical patterns I've applied across 4 AI/ML product lines |
| [`ml-product-lifecycle.md`](./frameworks/ml-product-lifecycle.md) | Managing ML products through build-measure-learn with degradation awareness |
| [`confidence-threshold-design.md`](./frameworks/confidence-threshold-design.md) | The automation pattern: confidence scores → graduated human involvement |

---

## Numbers That Matter

| Metric | Scale |
|--------|-------|
| **Portfolio value** | $90M+ annual recovered value + $20M+ predictive maintenance + $3.4M productivity |
| **Revenue influenced** | $2.4B in annual generation revenue through GenE |
| **Data scale** | 900M+ time-series records, 80GB/day ingestion, 10K+ API calls/min |
| **AI models in production** | 10,000+ per-device power surfaces, 3 document classifiers, 6+ predictive models |
| **User adoption** | 300+ DAU (GenE), product-led growth without mandates |
| **Cost structure** | 80% monitoring cost reduction (nuclear), $96K/yr infra savings (GCP migration) |
| **Charter ROI** | Profit indices from 25.8 to 81.2 across active workstreams |
| **Regulatory scope** | NRC-regulated nuclear + SOX/NERC compliance for financial reporting |

---

## How I Think About Product

| Principle | In Practice |
|-----------|-------------|
| **Portfolio over product** | I don't optimize one product in isolation. I allocate across four based on risk-adjusted value and strategic dependency. |
| **Thesis-driven** | "Every generation asset produces data that becomes a decision-making system." Every product maps back to this. |
| **Investment framework** | Every charter competes with quantified NPV and profit index. I say no to good ideas so we can ship great ones. |
| **Architecture as strategy** | I set technical direction (Rust, TimescaleDB, multi-agent AI, confidence gating) that others execute against and reuse. |
| **Trust engineering** | In regulated, high-stakes environments, trust is the product. Phased rollouts, human-in-the-loop, Go/No-Go gates. |
| **Build for adoption, not demos** | GTM is as important as the build. Phased rollout, training, parallel-run, adoption metrics, legacy retirement. |

---

## About

I build products at the intersection of AI, data platforms, and heavy industry. My career is defined by taking ambiguous, technically complex problems — where the data is messy, the stakeholders are skeptical, the regulatory environment is real, and the cost of failure is measured in millions — and turning them into shipped products that organizations depend on.

What distinguishes my work:
- **I operate at portfolio level.** Four independent products, different teams, different domains, unified by a shared thesis and investment framework.
- **I create businesses, not just products.** The GenE SaaS commercialization represents a new revenue line for a Fortune 200 company.
- **I set technical direction that scales.** Architecture patterns I established (Rust/TimescaleDB, multi-agent AI, confidence gating) are now the reference for adjacent teams.
- **I ship in regulated environments.** Nuclear (NRC), financial reporting (SOX/NERC), engineering compliance. These are not SaaS experiments — they are systems that run power plants.
- **I measure what matters.** Every initiative has a quantified business case. Every feature traces to a dollar value. Every quarter, I can show exactly where the portfolio stands against its targets.

**Open to:** AI product leadership, platform strategy, or roles where portfolio-level thinking, technical depth, and business impact converge.

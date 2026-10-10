# Framework: Enterprise Go-to-Market for Internal Products

## The Core Problem

Building a great internal product is half the job. Getting people to actually use it when they've been doing things their way for years, is the other half. Enterprise GTM requires the same rigor as external product launches, but with different levers.

This playbook is based on taking GenE from 30 to 300+ daily active users in 18 months without a usage mandate, and shipping DocIQ, Nuclear, and Fossil products into organizations that were skeptical of AI.

---

## The Playbook

### Phase 1: Find the Pain Champion

Don't start with the org chart. Start with the person whose job is hardest.

**What to do:**
- Identify the workflow that causes the most pain (hours wasted, errors made, frustration expressed)
- Find the person who suffers most from it. This is your pain champion, not your executive sponsor
- Spend time observing their actual workflow (not what they describe in a meeting)
- Quantify their pain in hours/week or dollars/month

**Why it matters:** Pain champions become evangelists. Executive sponsors give you budget. Pain champions give you credibility with the people who actually need to adopt.

**Example:** For GenE, the pain champion was the Asset Performance team doing month-end close. They spent 10+ days on spreadsheet reconciliation. When OpsReport automated that to Day 1, they became the loudest advocates for adoption across the fleet.

### Phase 2: Prove Value on the Hardest Problem First

Don't start with the easy sites or the friendly stakeholders. Start where the pain is worst.

**What to do:**
- Deploy to the highest-pain users first (largest fleet, most complex workflows, worst manual processes)
- Measure before/after on the specific pain metric (time-to-close, error rate, hours-per-task)
- Document the win with specific numbers, not testimonials

**Why it matters:** If it works for the hardest case, everything else is easier. And the hardest-case users become the most credible advocates ("if it works for us, it'll work for anyone").

**Example:** For GenE, I started with the most complex DTE workflows (highest manual burden). For DocIQ, I targeted drawings classification first (hardest category, 38 subtypes). For Nuclear, I required a Go/No-Go milestone before production deployment.

### Phase 3: Parallel-Run, Don't Hard-Cutover

Never take away the old system before the new one has proven itself.

**What to do:**
- Run both systems simultaneously for a defined period (usually 1-2 months)
- Track discrepancies between old and new outputs
- Let users compare results side-by-side
- Define exit criteria: what specific conditions must be met before the old system is retired?

**Why it matters:** Parallel-runs build trust. Users can verify the new system against their known-good process. When the new system matches or outperforms, they choose to switch. That's adoption, not compliance.

**Example:** For GenE, sites ran spreadsheets alongside OpsReport until they confirmed the numbers matched. For DocIQ, human reviewers validated AI classifications against their manual process before trusting auto-filing.

### Phase 4: Train by Persona, Not by Feature

Don't do a feature walkthrough. Train people on their workflow.

**What to do:**
- Identify distinct user personas (operator, analyst, manager, finance)
- For each persona, map their top 3 workflows in the new system
- Train on "how you do your job now" not "what buttons the system has"
- Provide quick-reference guides per persona, not a user manual

**Why it matters:** A site operator and a finance analyst use the same platform but need completely different training. Feature-focused training wastes everyone's time and leaves users confused about how the product fits their specific work.

### Phase 5: Measure Adoption, Intervene on Stalls

Track adoption at the granularity that matters and act when it stalls.

**What to do:**
- Define adoption metrics per site/team (DAU, workflow completion rate, time-to-task)
- Track weekly, not monthly
- When adoption stalls at a site, diagnose why (training gap? data quality issue? missing feature? change resistance?)
- Intervene specifically (not "let's do another training" but "this site has a data ingestion problem that makes the numbers look wrong")

**Why it matters:** Aggregate adoption metrics hide problems. A fleet-wide "200 DAU" number looks good until you realize 3 sites have zero usage because their data isn't flowing correctly.

### Phase 6: Retire the Old Way

The product isn't adopted until the old process is dead.

**What to do:**
- Set a retirement date for the old system/process (after parallel-run success criteria are met)
- Communicate the date clearly and repeatedly
- Remove access to legacy systems on the retirement date (don't leave them as fallbacks)
- Celebrate the transition as a milestone, not a mandate

**Why it matters:** As long as the old way exists, some users will use it. Legacy systems are comfortable. The parallel-run proves the new system works; retirement forces the final stragglers to switch.

---

## Common Failure Modes

| Failure Mode | What Happens | How to Prevent |
|-------------|-------------|---------------|
| **"Build it and they will come"** | Great product, zero adoption | GTM planning starts before build is complete |
| **Mandate without proof** | Forced adoption breeds resentment and workarounds | Prove value first, mandate only after the early adopters validate |
| **Training once** | People forget, new hires miss it, workflows evolve | Ongoing training, quick-reference guides, office hours |
| **Measuring features shipped, not adoption** | Team celebrates ship date while users ignore the product | Track DAU, task completion, and legacy-system retirement |
| **Ignoring data quality** | Users try the product, see wrong numbers, and never come back | Data quality is the first feature, not an afterthought |
| **Executive sponsor but no pain champion** | Budget secured but no one on the ground cares | Find the person whose life gets better, not just the person who signs the check |

---

## Metrics I Track

| Metric | What It Tells Me |
|--------|-----------------|
| **DAU by site/team** | Who's using it and who isn't |
| **Time-to-first-value** | How long from account creation to meaningful use |
| **Workflow completion rate** | Are people finishing tasks or abandoning mid-flow? |
| **Legacy system usage** | Is the old way dying? If not, why? |
| **Support ticket themes** | What's confusing people? (Clusters reveal training gaps) |
| **NPS by persona** | Operators vs. managers may have very different experiences |
| **Feature retention rate** | Are shipped features still being used 30/60/90 days later? |

---

## The Key Insight

Internal enterprise GTM is harder than external in one critical way: **your users didn't choose your product.** External customers evaluated alternatives and picked you. Internal users got told to use your thing instead of their spreadsheet.

That means you have to earn adoption through value, not through procurement. The moment you rely on a mandate instead of demonstrated value, you've lost the long game. Users will comply on the surface and work around you underneath.

The GenE story: 30 to 300+ DAU without a mandate: happened because the product solved a real pain point (month-end close) better than the alternative (spreadsheets). Every other adoption win flowed from that foundation.

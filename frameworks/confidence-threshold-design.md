# Framework: Confidence Threshold Design

## The Core Pattern

Most AI/ML products face the same tension: **automate for speed** vs. **review for accuracy**. Confidence thresholds resolve this by creating a graduated system:

```
High confidence  →  Automate (no human touch)
Medium confidence →  Route to review queue
Low confidence   →  Flag for expert review or reject
```

This isn't a novel idea, but the implementation details — where you set thresholds, how you adjust them, and what happens at the boundaries — make the difference between a system that works and one that fails silently.

## Design Principles

### 1. Thresholds are product decisions, not model decisions

The ML team can tell you the model's confidence distribution. But where to draw the line is a **business decision** that depends on:
- **Cost of a wrong automated decision** (a misclassified document vs. a wrong medical diagnosis)
- **Cost of human review** (salary * time per review * volume)
- **User tolerance for errors** (operations teams vs. end consumers)

As PM, I own the threshold decision. I set it based on the business case, not the model's ROC curve.

### 2. Thresholds must be adjustable without code deploys

If changing a threshold requires a code change, PR, review, and deploy — it won't get changed. Thresholds should be:
- Configurable via admin UI or environment variable
- Changeable by product/operations teams, not just engineers
- Audited (who changed it, when, and what was the previous value)

### 3. Changing a threshold should have immediate, visible effect

When you lower an automation threshold:
- Documents/items that now pass should be **re-queued for automation** (not stuck in limbo)
- The review queue should visibly shrink
- Dashboards should immediately reflect the change

When you raise a threshold:
- Previously-automated items in the pipeline should be **re-evaluated** against the new threshold
- Items that no longer pass should surface in the review queue

### 4. Monitor the boundaries, not just the averages

The most important metric isn't "what % of items are automated" — it's "what's the error rate among automated items." Specifically:

- **Automation error rate** — Of items that passed the threshold and were automated, how many were wrong? (Sampled via periodic human audit)
- **Review override rate** — Of items sent to review, how often does the reviewer agree with the model's prediction? (If it's >95%, your threshold is too conservative)
- **Boundary accuracy** — Model performance specifically for items near the threshold (within 5% confidence). This is where errors concentrate.

## Implementation Checklist

### For the PM
- [ ] Define the cost of a false positive (wrong automation) in business terms
- [ ] Define the cost of a false negative (unnecessary review) in business terms
- [ ] Set initial threshold conservatively (err toward more review early)
- [ ] Plan the cadence for threshold adjustment (monthly review of metrics)
- [ ] Define who has authority to adjust thresholds

### For the engineering team
- [ ] Confidence score attached to every prediction (0–1 continuous, not binned)
- [ ] Threshold stored as configuration (not hardcoded)
- [ ] Admin UI for threshold adjustment with audit log
- [ ] Re-evaluation trigger when threshold changes
- [ ] Dashboard showing: automation rate, review queue size, error rate by confidence band

### For operations/review teams
- [ ] Clear explanation of why an item was routed to review (confidence score visible)
- [ ] Ability to see the model's prediction alongside the review task
- [ ] Structured correction format (not just "reject" — capture the correct answer)
- [ ] Feedback on threshold-change impact ("if we lower by 5%, queue shrinks by N items/day")

## Common Traps

**Trap: Setting one threshold for all categories**
Different categories have different confidence distributions. A model might be 95%+ confident on Category A (lots of training data) but max out at 70% on Category B (few examples). A single threshold either over-automates B or under-automates A.
*Fix:* Per-category thresholds, or at minimum per-category monitoring.

**Trap: Never adjusting the threshold after launch**
The model improves over time (retraining from corrections). If the threshold never moves, you're paying for unnecessary reviews forever.
*Fix:* Scheduled threshold reviews (monthly or quarterly) with data on error rates and queue volumes.

**Trap: Confidence ≠ correctness**
A model can be confidently wrong — especially on out-of-distribution inputs. High confidence doesn't guarantee correctness.
*Fix:* Periodic random audits of automated items (not just review-queue items). Sample 1–5% of automated decisions for human verification.

## When This Pattern Doesn't Apply

- **All-or-nothing decisions** — If there's no meaningful "medium confidence" zone (e.g., safety-critical binary decisions), thresholds may not help. You need a different pattern (e.g., dual-model agreement).
- **Low-volume tasks** — If the total volume is small enough for a human to review everything, the complexity of threshold management isn't worth it. Just review everything.
- **Rapidly changing domains** — If the underlying data distribution shifts faster than you can retrain, confidence scores become unreliable. Focus on drift detection instead.

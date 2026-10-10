# Framework: ML Product Lifecycle Management

## Overview

Managing ML products differs fundamentally from managing traditional software products. Models degrade, data drifts, and "done" doesn't exist. There's only "good enough for now." This framework captures how I manage ML products through their lifecycle.

## The Four Phases

### Phase 1: Problem Validation
**Goal:** Confirm that ML is the right solution and that the data exists.

Before writing a single line of model code:
- **Define the business metric**: not model accuracy, but the operational outcome (time saved, errors prevented, dollars recovered)
- **Audit the training data**: Is there enough labeled data? Is it representative? What's the labeling quality?
- **Establish the human baseline**: How well do humans perform this task today? If human performance is 80%, a model at 85% is a meaningful improvement. A model at 95% might not be worth the investment over a simpler rules-based approach.
- **Define "good enough"**: What accuracy threshold unlocks the business value? This is rarely 99%.

### Phase 2: Build & Validate
**Goal:** Ship a model that meets the "good enough" threshold with a clear measurement framework.

Key product decisions at this phase:
- **Evaluation framework first**: Before training, define the held-out test set, the metrics (F1, precision, recall: and which matters more for this use case), and the comparison baseline
- **Experiment tracking**: Every training run logged with parameters, metrics, and artifacts (I use MLflow). No model ships without a tracked comparison to the previous version.
- **Confidence scoring**: Every prediction must include a confidence signal. This is non-negotiable: it's what enables Phase 3 automation.
- **Error analysis**: Don't just report aggregate accuracy. Break it down by category, by edge case, by data source. The aggregate number hides the problems.

### Phase 3: Operationalize
**Goal:** Move from "model works in a notebook" to "model runs in production with appropriate automation."

Key product decisions:
- **Confidence thresholds**: High-confidence predictions are automated; low-confidence predictions go to human review. The threshold is adjustable without a code deploy.
- **Monitoring & alerting**: Track prediction distribution drift, confidence score distribution, and human override rate. Alert when any shifts significantly.
- **Graceful degradation**: When the model fails or confidence drops below threshold, the system defaults to human handling, not silent failure.
- **Audit trail**: Every prediction is traceable to the model version, input data, and confidence score that produced it.

### Phase 4: Continuous Improvement
**Goal:** Use production feedback to systematically improve the model over time.

Key product decisions:
- **Feedback collection design**: Human corrections must be captured in a format that's directly usable for retraining. This means structured corrections (not just "this was wrong" but "the correct answer is X").
- **Retraining triggers**: Define what triggers retraining: correction volume threshold, accuracy drift detected, or scheduled cadence? I prefer threshold-based (retrain when N corrections accumulate) with a scheduled floor (retrain at least monthly).
- **Model promotion gates**: New model must beat the current production model on the held-out test set AND on recent corrections before deployment. No automatic promotion without comparison.
- **Versioning & rollback**: Every model version is tagged and deployable. Rollback is a single operation, not a re-training exercise.

## Anti-Patterns I Watch For

| Anti-Pattern | Why It's Dangerous |
|---|---|
| Optimizing for aggregate accuracy | Hides poor performance on minority categories that matter to users |
| No confidence scoring | Forces a binary ship/don't-ship decision instead of enabling graduated automation |
| Manual retraining | Creates drift between model performance and user expectations; corrections pile up without effect |
| Accuracy as the only metric | Ignores latency, cost, interpretability, and operational fit |
| "We'll add monitoring later" | By the time you notice drift, users have already lost trust |

## When NOT to Use ML

ML is expensive to build and maintain. I actively advocate against ML when:
- A rules-based approach achieves 90%+ of the value with 10% of the complexity
- The labeled dataset is too small or too noisy to train a reliable model
- The decision being automated has catastrophic failure modes and no confidence threshold can make it safe
- The business case doesn't justify ongoing model maintenance costs

# Risk Register

| Risk | Why it matters | Mitigation |
|---|---|---|
| Small sample | 12 rows are insufficient for reliable generalization | Collect a larger representative dataset |
| Plan imbalance | Basic is 100% churned in this sample, while Pro/Standard are 0% | Do not infer population-wide effects; test on larger data |
| Data leakage | Timing of feature collection is undocumented | Define prediction point and enforce time-based feature availability |
| False positives | Non-churners may receive unnecessary intervention | Monitor precision and review flagged cases |
| False negatives | Churners may be missed | Monitor recall and review missed cases |
| Privacy | `customer_id` identifies records | Exclude ID from features and restrict access |
| Automation misuse | Predictions could become automatic decisions | Keep humans responsible for consequential actions |

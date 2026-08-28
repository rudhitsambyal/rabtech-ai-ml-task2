# Responsible Data Card

## Dataset purpose
This dataset supports an exploratory baseline for predicting customer churn. It may be used to identify patterns associated with churn and to prioritize customers for further analysis or supportive retention outreach. It must not be used by itself to automatically cancel services, deny support, or make high-impact decisions without human review.

## Provenance and permission
The provided file is a small training dataset supplied for the RabTech Academy ML problem-framing exercise. The available source material does not document the real-world collection process, consent status, licensing terms, or named data owner. These items should be confirmed before production use. Access should be limited to authorized project users.

## Population and representation
The dataset contains 12 customer records. It represents only the customers included in this training sample and should not be assumed to represent the full customer population. Churned customers are 5/12 (41.7%) and non-churned customers are 7/12 (58.3%). Plan types are Basic, Standard, and Pro; in this small sample all Basic customers churned while no Standard or Pro customers churned, which may indicate sampling imbalance and should not be treated as a general population effect.

## Features and target
- `customer_id`: customer identifier. Use for record tracking only; exclude from model features.
- `tenure_months`: length of customer relationship in months.
- `support_tickets`: number of support tickets.
- `monthly_spend_inr`: monthly spend in INR.
- `last_login_days`: days since last login.
- `plan_type`: subscription plan category.
- `churned`: binary target label (1 = churned, 0 = not churned).

Potential leakage: the dataset does not document the timing of feature collection relative to the churn event, so leakage cannot be ruled out without confirming that every feature was available before the prediction point. Sensitive attributes are not explicitly provided, but plan type, spending, and engagement variables could act as indirect proxies for customer characteristics in some settings.

## Quality checks
- Missing values: none in the 12 rows or 7 columns.
- Exact duplicate rows: none.
- Duplicate customer IDs: none.
- Numeric ranges in this sample: tenure 1–30 months; support tickets 0–5; monthly spend ₹499–₹1,499; last login 1–30 days.
- Class balance: 7 non-churned (58.3%) vs 5 churned (41.7%).
- Train/test separation: no train/test split is provided in the source file. Because the dataset has only 12 rows, any split would be unstable; a larger dataset is required for reliable validation.

## Risks and safeguards
- Bias risk: the sample is tiny and plan types are strongly associated with the target. Mitigation: collect a representative dataset and evaluate error rates across relevant customer groups.
- Privacy risk: customer identifiers are present. Mitigation: exclude identifiers from modeling and restrict access.
- Misuse risk: predictions could be treated as facts. Mitigation: use predictions as decision support and require human review for consequential actions.
- False positives: customers may be incorrectly flagged as likely to churn. Mitigation: monitor precision, review false-positive cases, and avoid punitive actions.
- False negatives: at-risk customers may be missed. Mitigation: monitor recall and use a non-ML baseline alongside the model.

## Intended evaluation
Before training, define:
- Baseline: majority-class prediction and a simple rule-based baseline.
- Performance: accuracy plus precision, recall, F1, and ROC-AUC where the sample size permits.
- Calibration: compare predicted probabilities with observed outcomes on a suitably sized validation set.
- Fairness: compare relevant error rates and selection rates across meaningful customer groups once those groups are appropriately represented.
- Error analysis: review false positives and false negatives separately, including their plan type and behavioral characteristics.

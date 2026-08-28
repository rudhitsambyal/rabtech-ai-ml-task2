# ML Problem-Framing Memo

## Decision
The business wants to identify customers who are more likely to churn so that the retention team can prioritize timely, appropriate outreach.

## Prediction target
Predict `churned` (1/0).

## Unit of observation
One customer record.

## Prediction timing
The exact prediction point is not documented in the supplied training data. For a production model, features must be frozen at a clearly defined prediction date and only information available before that date may be used.

## Action window
A practical pilot could use a short retention-outreach window after scoring, with the exact period defined by the business process.

## Non-ML baseline
Start with:
1. Majority-class prediction.
2. A simple rule-based flag, for example prioritizing customers with high `last_login_days` and/or high `support_tickets`.

## Why ML may be justified
The sample shows strong relationships between churn and behavioral variables. Churned customers in this sample have lower average tenure, more support tickets, lower monthly spend, and many more days since last login. A larger, representative dataset is required before concluding that these relationships generalize.

## Main harms
Incorrectly flagging customers can waste outreach effort or create an unwanted customer experience. Missing at-risk customers can reduce the effectiveness of retention activity. Using customer attributes without fairness and privacy checks can create unequal treatment.

## Fallback
If the model fails quality or fairness checks, use the documented non-ML baseline and human review rather than automatically deploying the model.

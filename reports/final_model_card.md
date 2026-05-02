# Final Fraud Detection Model Card

## Selected Model

- Model: XGBoost
- Saved file: `models/final_model.pkl`
- Decision threshold: 0.89896
- Selection score: 0.8239

## Why This Model Was Selected

This model was selected because it passed the required gates and had the best weighted balance of fraud-catching ability, precision, ranking quality, and generalization stability.

The most important project constraint is the class imbalance: fraud cases are extremely rare, so accuracy is not meaningful as a decision metric. The selected model is judged by precision, recall, F2, ROC-AUC, average precision, false positives, false negatives, and overfitting gap.

## Final Test Metrics

- Precision: 0.9867
- Recall: 0.7789
- F1: 0.8706
- F2: 0.8132
- ROC-AUC: 0.9683
- Average precision: 0.8114
- False positives: 1
- False negatives: 21
- Overfit gap: 0.0317

## Intended Use

The model is intended to rank credit card transactions by fraud risk and flag transactions above the selected threshold for review or downstream action.

## Preprocessing Assumptions

- Use the same preprocessing flow from `02_preprocessing.ipynb`.
- Use the saved scaler and feature order from the processed training data.
- Do not fit preprocessing steps on future test or production data.
- Keep raw and processed data local; the `data/` folder is ignored by Git.

## Limitations

- The dataset is highly imbalanced, so small changes in threshold can materially change false positives and false negatives.
- The model was evaluated on historical data and should be monitored for drift.
- The selected threshold reflects the current balance between catching fraud and limiting review workload. A different business cost policy may choose a different threshold.

## Monitoring Recommendation

Track precision, recall, false positives, false negatives, fraud base rate, score distribution, and feature drift over time. Re-tune the threshold if the fraud base rate or investigation capacity changes.
# Lab 4 Report – Explainable and Privacy-Aware AI Threat Alert

**Student Name:** Aniket Singh
**Roll Number:** 2501012308
**Course:** ENSP355 – AI in Cyber Security  
**Institution:** K.R. Mangalam University, School of Engineering & Technology  
**Academic Year:** 2026–27

## Aim
To generate confidence-aware login predictions, explain the model using feature importance, test sensitivity to one controlled input change, mask identifiers, and produce responsible alerts with human-review guidance.

## Dataset and model
The available earlier synthetic login-activity dataset contains 100 rows: 70 Normal records (label 0) and 30 Suspicious records (label 1). Its `data_transfer_mb` column is renamed to `download_mb` to match the Lab 4 manual. The original Lab 2 model file was not included with the uploaded PDF, so the Decision Tree was retrained using `DecisionTreeClassifier(max_depth=4, random_state=42)` and a stratified 75/25 split with `random_state=42`.

The test accuracy for this reproducible split is **88.00%**. The confusion matrix, with rows/columns ordered as Normal then Suspicious, is:

| Actual / Predicted | Normal | Suspicious |
|---|---:|---:|
| Normal | 16 | 2 |
| Suspicious | 1 | 6 |

## Q1. Baseline predictions with confidence (5 marks)

| Account ID | Failed logins | Login hour | New device | Download MB | Prediction | Confidence |
|---|---:|---:|---:|---:|---|---:|
| ACC-1001 | 0 | 10 | 0 | 40 | Normal | 1.000 |
| ACC-1002 | 7 | 2 | 1 | 150 | Suspicious | 1.000 |
| ACC-1003 | 1 | 15 | 0 | 720 | Suspicious | 1.000 |
| ACC-1004 | 4 | 23 | 1 | 400 | Suspicious | 1.000 |
| ACC-1005 | 2 | 9 | 0 | 80 | Normal | 1.000 |

**Lowest-confidence record:** All five records tie at 1.000, so there is no unique lowest-confidence record.

**Why confidence is not certainty:** Confidence is the model's estimated probability for its selected class. It is not proof that an event is safe or malicious; the model is trained on a small synthetic dataset and can be wrong or overconfident.

## Q2. Feature importance and explanation (10 marks)

| Feature | Importance |
|---|---:|
| download_mb | 0.8221 |
| failed_logins | 0.1779 |
| login_hour | 0.0000 |
| new_device | 0.0000 |

**Top-three explanations:**
1. `download_mb`: Download volume was the most influential feature in this fitted tree.
2. `failed_logins`: Failed login attempts were the second most influential feature.
3. `login_hour`: Login hour had zero importance in this fitted tree; it was not used for its splits.

The notebook includes the labelled feature-importance bar chart.

**Caution:** Feature importance describes how the fitted model used inputs. It does not prove that a feature causes suspicious activity.

## Q3. Controlled sensitivity test (10 marks)

The fifth baseline record was copied. Only `failed_logins` was changed from 2 to 8; login hour, device status and download volume remained unchanged.

| Case | Failed logins | Prediction | Confidence |
|---|---:|---|---:|
| Baseline | 2 | Normal | 1.000 |
| Changed | 8 | Suspicious | 1.000 |

**Interpretation:** Increasing failed login attempts from 2 to 8 changes the prediction from Normal to Suspicious. This shows that the fitted tree is sensitive to the failed-login feature. Confidence remains 1.000 because the two records reach pure training leaves; this is a limitation of a small tree trained on a small dataset, not a guarantee of correctness.

## Q4. Privacy masking and responsible-use rules (5 marks)

Masking examples:
- `192.168.10.24` → `192.168.xxx.xxx`
- `ACC-1002` → `ACC-***02`

The masked table in the notebook displays only masked account IDs and masked IP addresses, along with prediction and confidence.

**Four privacy/responsible-use rules:**
1. Mask identifiers before display or export.
2. Use sanitized data in classroom notebooks.
3. Restrict access to unmasked records.
4. Require human review for high-risk action.

## Q5. Responsible alert generation (10 marks)

| Account | Prediction | Severity | Reason | Recommended action | Human review |
|---|---|---|---|---|---|
| ACC-***01 | Normal | Low | no strong warning | Continue normal monitoring. | No |
| ACC-***02 | Suspicious | High | many failed logins, new device, unusual login time | Verify, contain if required, and report. | Yes |
| ACC-***03 | Suspicious | High | large data download | Verify, contain if required, and report. | Yes |
| ACC-***04 | Suspicious | High | new device, unusual login time | Verify, contain if required, and report. | Yes |
| ACC-***05 | Normal | Low | no strong warning | Continue normal monitoring. | No |

**Human-review condition:** Human review is set to Yes for High and Medium severity alerts. The prototype does not automatically block accounts or punish users.

**Limitation:** The model uses a small synthetic classroom dataset and a limited set of numeric features. Real security decisions require additional context, validation on representative data, and analyst review.

## Conclusion
The lab demonstrates explainable and privacy-aware alerting. Confidence values accompany baseline predictions, feature importance provides a model-level explanation, and the controlled test shows how changing one feature can change a decision. Identifiers are masked before display, and final alerts include severity, reason, recommended action and human-review status. Confidence supports but does not replace human judgement.

## Submission evidence checklist
- [x] Five baseline predictions with confidence
- [x] Feature-importance table and chart
- [x] Controlled before/after sensitivity result
- [x] Masked identifiers and four privacy rules
- [x] Final alert with severity, reason, action and human review
- [x] Conclusion
- [ ] Add your shareable Google Colab link after uploading and running the notebook in your own Colab account

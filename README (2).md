# Cybersecurity Lab Assignment 4
## Explainable and Privacy-Aware AI Threat Alert

**Student:** Prince kumar
**Roll Number:** 2401010198
**Course:** ENSP355 – AI in Cyber Security  
**Institution:** K.R. Mangalam University, School of Engineering & Technology  
**Academic Year:** 2026–27

This repository implements Lab 4 from the supplied lab manual. It covers:
1. Five baseline Normal/Suspicious predictions with model confidence.
2. Decision Tree feature importance and plain-language explanations.
3. A controlled sensitivity test changing only `failed_logins` from 2 to 8.
4. Masking account IDs and IP addresses, plus four responsible-use rules.
5. Responsible alerts with severity, reason, recommended action, and human-review status.

## Files
- `simple_cyber_activity.csv` – synthetic login-activity dataset.
- `lab4_explainable_privacy_alert.py` – complete runnable Python solution.
- `Lab4_Explainable_Privacy_Aware_Threat_Alert.ipynb` – notebook version for Google Colab.
- `Lab_Report.md` – written answers, output interpretation, and conclusion.
- `requirements.txt` – Python dependencies.

## Dataset and model note
The available earlier synthetic login-activity CSV used the field `data_transfer_mb`; it is renamed to `download_mb` in this Lab 4 copy to match the supplied Lab 4 manual. The manual says to load or retrain the Lab 2 Decision Tree. The original Lab 2 model file was not included with the uploaded Lab 4 PDF, so this solution retrains a reproducible `DecisionTreeClassifier(max_depth=4, random_state=42)` on the available 100-row synthetic dataset, using a stratified 75/25 train/test split (`random_state=42`). If your instructor's Lab 2 dataset differs, replace the CSV and rerun the notebook/script.

## Run in Google Colab
1. Upload this repository's notebook and CSV to Colab.
2. Upload `simple_cyber_activity.csv` into the Colab session.
3. Select **Runtime → Run all**.
4. Save the executed notebook and share its Colab link with your instructor.

## Run locally
```bash
pip install -r requirements.txt
python lab4_explainable_privacy_alert.py
```

## Responsible-use note
The dataset is synthetic and intended for classroom demonstration only. Model confidence is not certainty. Do not automatically block or punish accounts based on this prototype; high-risk or uncertain alerts require human review.

Prince kumar
2401010198

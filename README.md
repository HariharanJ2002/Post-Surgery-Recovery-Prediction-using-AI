# 🏥 Post-Surgery-Recovery-Prediction-using-AI

## Overview

Recovery after open-heart surgery is complex, highly individualized, and often difficult to monitor once patients leave the hospital. Our team built a robust, clinically-informed AI system that leverages **wearable sensor data** and **treadmill cardiopulmonary assessments** to forecast:

- Expected recovery duration (in days)
- Risks of delayed rehabilitation
- Personalized rehab support needs

At the core of this project is a hybrid modeling architecture that bridges **physiological insight** with **machine learning precision**—designed to complement clinical judgment, not replace it.

---

## Why This Matters

Despite advances in surgical technique, post-op care too often depends on **generic timelines and reactive interventions**. By integrating **real-time biometric signals** with recovery trajectories validated by cardiopulmonary benchmarks, this work offers:

- Early detection of **recovery deviation**
- Clinically interpretable predictions
- Personalized recovery timelines grounded in evidence-based rehab targets

---

## 📂 Project Directory Structure
---
```bash
post-op-recovery-ai/
├── data/
│   ├── treadmill_test_measure.xlsx
│   └── wearabledata/
│       ├── acc/
│       ├── ecg/
│       ├── Wearable_subject-info.xlsx
│       └── Wearable_test-availability.xlsx
│
├── models/
│   ├── cardiac_rf_model.pkl
│   ├── cardiac_rf_model_clean.pkl
│   ├── mobility_xgb_model.pkl
│   ├── mobility_rf_generalized_model.pkl
│   ├── mobility_xgb_model_clean.pkl
│   ├── hybrid_meta_model.pkl
│   ├── hybrid_meta_model_v2.pkl
│   └── hybrid_meta_model_v3.pkl
│
├── notebooks/
│   ├── cardiac_model.ipynb
│   ├── ecg_features.ipynb
│   ├── mobility_model.ipynb
│   ├── mobility_model_v2.ipynb
│   ├── hybrid_model_V1.ipynb
│   ├── hybrid_model_V2.ipynb
│   ├── hybrid_model_V3.ipynb
│   ├── rehab_using_V1.ipynb
│   └── rehab_using_V2.ipynb
│
├── results/
│   ├── ecg_features1.xlsx
│   ├── rehab_batch_report.xlsx
│   ├── rehab_batch_report_using_V2.xlsx
│   ├── rehab_batch_report_using_V3.xlsx
│   └── rehab_test_cases.xlsx
│
└── README.md
```

---

## Model Pipeline

### 🧠 1. Cardiac Recovery Model
- **Inputs**: VO₂ max, heart rate recovery (HRR 60s), VE/VO₂, ECG-derived features
- **Model**: Random Forest Regressor
- **Output**: Cardiac recovery score
- **Performance**: R² = 0.868 | MSE = 0.48

### 🦿 2. Mobility Recovery Model v2 (Biomechanical Enhanced)
- **Inputs**: Stride width, stance time, gait symmetry, cadence
- **Model**: XGBoost Regressor (with SHAP overlays)
- **Output**: Functional mobility recovery score
- **Performance**: R² = 0.984 | MSE = 0.0134

### 🧩 3. Hybrid Meta-Model (Final)
- **Inputs**: Standardized cardiac + mobility recovery scores
- **Formula**:  
  ```python
  Recovery_Days = 210 - (Score × 60)
  ```
- **Output**: Personalized recovery time (30–180 days)
- **Performance**: R² = 0.9912 | MSE = 0.005

---

## How to Run the Project

> ✅ Python 3.9+ recommended. Notebooks assume a Unix-style path layout.

### 1. Clone the repo
```bash
git clone https://github.com/AJ-pmn09/post-op-recovery-ai.git
cd post-op-recovery-ai
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Launch & Run Notebooks
```text
notebooks/ecg_features.ipynb           # ECG + HRV signal preprocessing
notebooks/cardiac_model.ipynb          # VO2 + ECG-based recovery scoring
notebooks/mobility_model_v2.ipynb      # Gait-based biomechanical recovery
notebooks/hybrid_model_V3.ipynb        # Final score-to-recovery-day mapping
notebooks/rehab_using_V2.ipynb         # Batch predictions on new subjects
```

### 4. Update file paths if needed
Most files load from `../data/` or `../results/`, e.g.:

```python
pd.read_excel('../data/wearabledata/Wearable_subject-info.xlsx')
pd.read_excel('../results/rehab_batch_report_using_V3.xlsx')
```

---

## Results & Deliverables

### 📈 Predictions Available:
- `results/rehab_batch_report_using_V3.xlsx`  
  → Contains per-subject recovery durations and feature-level scores

- `results/rehab_test_cases.xlsx`  
  → Internal validation on unseen subjects

- `results/ecg_features1.xlsx`  
  → Derived HRV and ECG morphology used in training

### 📁 Trained Models
Stored in `/models/`:
- `cardiac_rf_model.pkl`
- `mobility_xgb_model.pkl`
- `hybrid_meta_model_v3.pkl`

---

## Clinical Relevance

This system does **not assume clinical diagnosis**. Instead, it serves as an augmentation layer:

- For clinicians managing **home-based cardiac rehab**
- For patients needing a **customized recovery window**
- For research teams evaluating **frailty and recovery prediction models**

Each prediction is explainable via **SHAP plots**, ensuring interpretability and transparency.

---

## What's Next

We’re planning to:
- Replace batch inference with real-time streaming (ECG and accelerometer)
- Deploy explainable recovery predictions into clinician dashboards (EPIC API integration)
- Extend generalization using longitudinal gait datasets from multi-site trials

---

## Authors

- **Hariharan Jothimani**  
- **Madhava Narasimha Ajay Varma Penmatsa**  

> We believe the future of recovery is not just automated—it's adaptive, interpretable, and personal.

---

## Dataset Link

<h2>Wearable-based signals during physical exercises from patients with frailty after open-heart surgery.</h2>

-  Sokas, Daivaras, et al. "Wearable-based signals during physical exercises from patients with frailty after open-heart surgery" (version 1.0.0). PhysioNet (2022),https://doi.org/10.13026/mp8k-7p27.
-  Link: https://physionet.org/content/wearable-exercise-frailty/1.0.0/

<h2>Treadmill Maximal Exercise Tests from the Exercise Physiology and Human Performance Lab of the University of Malaga</h2>

-  Mongin, Denis, et al. "Treadmill Maximal Exercise Tests from the Exercise Physiology and Human Performance Lab of the University of Malaga" (version 1.0.1). PhysioNet 
  (2021), https://doi.org/10.13026/7ezk-j442.
  
-  Link: https://physionet.org/content/treadmill-exercise-cardioresp/1.0.1/


---

## Contact

📬 For collaborations, clinical validation, or demo requests:  
`mpenmats@mtu.edu.com`
`hjothima@mtu.edu.com`

---

## 🎥 Presentation & Demo

We’ve put together a full walkthrough of the system — from problem motivation to model deployment and real-world use cases:

- Clinical relevance and recovery time forecasting  
- Dataset preparation (ECG, gait, VO₂, frailty)  
- Model development and hybrid scoring  
- SHAP-based explainability for decision transparency

👇 **Click to watch the presentation**:

[![Watch on YouTube](https://img.youtube.com/vi/-g9pWO-qbjo/hqdefault.jpg)](https://www.youtube.com/watch?v=-g9pWO-qbjo)

> 📺 **Link**: [https://www.youtube.com/watch?v=-g9pWO-qbjo](https://www.youtube.com/watch?v=-g9pWO-qbjo)

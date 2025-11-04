# A-Project: Personality Classification & Model Monitoring with Vertex AI

This project developed an **AutoML personality classification model** using **Google Vertex AI**, predicting whether users are **introverts or extroverts** based on social and behavioral traits.  
The full pipeline included **dataset creation**, **model training**, **evaluation**, **deployment**, and **automated monitoring** to ensure long-term reliability and fairness.

* **Dataset:** 2,900 records, 8 behavioral and social features (e.g., Post Frequency, Friends Circle Size, Stage Fear).  
* **Tools:** Google Vertex AI AutoML, Cloud Monitoring, Python, JSON logs.  
* **Techniques:** AutoML classification, confidence threshold tuning, model deployment, and drift detection via monitoring jobs.  
* **Goal:** Demonstrate responsible AI deployment with explainability and drift tracking.

---

### 🧱 Model Creation

**1. Dataset Upload**
- Uploaded the CSV dataset to **Vertex AI Datasets** in Google Cloud Storage.  
- Automatically parsed schema with columns such as:
  - `Post_frequency`, `Social_event_attendance`, `Stage_fear`, `Friends_circle_size`, `Time_spent_alone`, `Stress_level`.  
- Labeled the **target column**: `Personality` → *Introvert* or *Extrovert*.  

**2. AutoML Training**
- Used **Vertex AI AutoML Classification** (no-code training).  
- Enabled automatic feature engineering and model tuning.  
- Ran multiple experiments with two confidence thresholds:
  - **0.5** (balanced accuracy vs. coverage)
  - **0.8** (higher precision, lower recall)

**3. Evaluation**
- Vertex AI generated precision–recall and confusion matrix visualizations.  
- **Best model:** 0.5 threshold → optimal for user-friendly applications.  
- **Results:**
  - Accuracy: **93–94%**
  - Introvert recall improved from **93% → 94%**
  - Reduced false positives (Introverts misclassified as Extroverts) from **7% → 6%**

<div align="center">
  <img src="images/vertex_training_evaluation.png" alt="Vertex AI AutoML Training Evaluation" width="600"/>
  <p><em>Model evaluation in Vertex AI AutoML showing improved introvert recall and balanced precision.</em></p>
</div>

---

### 🧩 Feature Attribution (Explainability)

**Top Features (SHAP Analysis)**  
| Feature | Importance | Interpretation |
|----------|-------------|----------------|
| Post_frequency | ⭐ Highest | High posting frequency = Extroversion |
| Social_event_attendance | ⭐⭐ | Social activity drives Extrovert classification |
| Stage_fear | ⭐⭐ | Low stage fear → Extrovert; high fear → Introvert |
| Time_spent_alone | ⭐ | Longer time alone → Introversion |
| Friends_circle_size | ⭐ | Moderate indicator of social confidence |

<div align="center">
  <img src="images/vertex_feature_attribution.png" alt="Feature Attribution Plot" width="600"/>
</div>

---

### 🧩 Model Monitoring Configuration

**Monitoring Components**
- **Input Drift:** Detects distribution shifts in features.  
- **Prediction Drift:** Identifies output pattern shifts over time.  
- **Attribution Drift:** Detects evolving feature importance patterns.  

**Implementation**
- Configured via **Vertex AI Monitoring**:
  - Drift threshold = 0.3  
  - Enabled **email alerts** on drift detection  
  - Sampling rate: 100% (all predictions logged)  
- Used **Google Cloud Shell** commands to update monitoring jobs and log prediction drift in JSON format.  

<div align="center">
  <img src="images/vertex_monitoring_overview.png" alt="Vertex AI Monitoring Overview" width="600"/>
</div>

---

### 📉 Drift Detection Results

| Feature | Issue | Interpretation |
|----------|--------|----------------|
| Drained_after_socializing | All “Yes” | Schema mismatch – skewed data |
| Friends_circle_size | All = 100 | Default input causing inflated extroversion |
| Post_frequency | Attribution drift > 0.1 | Overweighted feature |
| Stage_fear | All “Yes” | Parsing error, categorical imbalance |
| Social_event_attendance | Increased | Seasonal/social pattern bias |

<div align="center">
  <img src="images/vertex_input_drift.png" alt="Input Drift Example" width="450"/>
  <img src="images/vertex_attribution_drift.png" alt="Feature Attribution Drift" width="450"/>
</div>

---

### 🎯 Key Takeaways
- **AutoML enabled fast and accessible modeling**, ideal for small teams.  
- **Model monitoring ensured trustworthiness** by detecting data shifts early.  
- **Explainability (SHAP)** supported responsible AI interpretation.  
- Framework applicable to social platforms, HR analytics, and CRM recommendation systems.  

---

### 🧠 Skills Demonstrated
- Google Vertex AI AutoML training, tuning, and deployment  
- Feature attribution and explainable AI (SHAP)  
- Model drift detection and governance  
- MLOps monitoring configuration with Google Cloud  

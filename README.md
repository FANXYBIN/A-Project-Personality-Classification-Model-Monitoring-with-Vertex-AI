# A-Project: Personality Classification & Model Monitoring with Vertex AI

This project developed an **AutoML personality classification model** using **Google Vertex AI**, predicting whether users are **introverts or extroverts** based on social and behavioral traits.  
The model lifecycle included **training, evaluation, deployment, and automated monitoring** to detect input drift, prediction drift, and feature attribution drift.

* **Dataset:** 2,900 records, 8 behavioral and social features (e.g., Post Frequency, Friends Circle Size, Stage Fear).  
* **Tools:** Google Vertex AI AutoML, Cloud Monitoring, Python, JSON logs.  
* **Techniques:** AutoML classification, confidence threshold tuning, model deployment, and drift detection via monitoring jobs.  
* **Goal:** Demonstrate responsible AI deployment with explainability and drift monitoring.

---

### ⚙️ Model Development

**Model Training**
- Used Vertex AI AutoML to train a binary classifier (Extrovert vs. Introvert).  
- Tuned **confidence thresholds (0.5 & 0.8)** — 0.5 gave best accuracy–coverage balance.  
- Improved introvert classification accuracy from **93% → 94%** and reduced misclassifications by 1%.  

**Feature Attribution (SHAP-based Explainability)**
- `Post_frequency`: Highest feature influence.  
- `Social_event_attendance` and `Stage_fear`: Key behavioral differentiators.  
- `Friends_circle_size` and `Time_spent_alone`: Moderate influence, indicating social engagement and isolation dynamics.  

---

### 🧩 Model Monitoring Configuration

**Monitoring Components**
- **Input Drift:** Detects changes in raw feature distributions.  
- **Prediction Drift:** Flags shifts in output probability patterns.  
- **Attribution Drift:** Measures changing feature importance over time.  

**Implementation**
- Configured via Vertex AI Monitoring with:
  - Drift threshold = **0.3** (Jensen–Shannon divergence)
  - Email alerts for drift exceedance  
  - Endpoint logging with 100% sampling rate  

<div align="center">
  <img src="images/vertex_monitoring_overview.png" alt="Vertex AI Monitoring Overview" width="600"/>
  <p><em>Vertex AI drift detection dashboard monitoring input and attribution changes.</em></p>
</div>

---

### 📉 Drift Detection Results

| Feature | Issue | Interpretation |
|----------|--------|----------------|
| **Drained_after_socializing** | All "Yes" | Schema mismatch; inflated feature weighting. |
| **Friends_circle_size** | All = 100 | UI bug or default value inflating extroversion inference. |
| **Post_frequency** | Attribution drift > 0.1 | Model overweights this feature under uniform inputs. |
| **Stage_fear** | All "Yes" | Parsing error; skewed categorical input. |
| **Social_event_attendance** | High participation | Seasonal/sampling bias; model dependency increased. |

<div align="center">
  <img src="images/vertex_input_drift.png" alt="Input Drift Example" width="450"/>
  <img src="images/vertex_attribution_drift.png" alt="Feature Attribution Drift" width="450"/>
</div>

---

### 🔍 Key Takeaways
- **AutoML = speed + accessibility:** Enabled rapid, no-code model development.  
- **Monitoring = reliability:** Detected schema mismatches, feature bias, and evolving behavior patterns.  
- **Responsible AI:** Combined explainability and drift tracking for transparent model governance.  
- **Business Relevance:** Similar pipelines can enhance social apps, CRM systems, and recruitment platforms.  

---

### 🧠 Skills Demonstrated
- Vertex AI AutoML training & deployment  
- Data drift and attribution drift monitoring  
- Model governance and explainability (SHAP, JSON logs)  
- MLOps workflow for responsible AI  


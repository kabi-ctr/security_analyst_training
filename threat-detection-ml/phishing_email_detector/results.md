# Detection Results

This document summarizes the performance of multiple machine learning models used to detect phishing emails based on email text content.

---

## Dataset Summary
- Total samples: 5,572 emails
- Classes:
  - Legitimate (ham)
  - Phishing (spam)
- Train–test split: 80% / 20%
- Feature extraction: TF-IDF (5,000 features)

---

## Model Performance Comparison

### Logistic Regression
- Accuracy: **95.87%**
- Precision (weighted avg): **0.96**
- Recall (weighted avg): **0.96**
- F1-score (weighted avg): **0.96**

**Observation:**  
A strong baseline model with balanced performance and low computational cost.

---

### Multinomial Naive Bayes
- Accuracy: **97.31%**
- Precision (weighted avg): **0.97**
- Recall (weighted avg): **0.97**
- F1-score (weighted avg): **0.97**

**Observation:**  
Performs very well for text classification tasks and handles word-frequency features efficiently.

---

### Support Vector Machine (SVM)
- Accuracy: **97.94%**
- Precision (weighted avg): **0.98**
- Recall (weighted avg): **0.98**
- F1-score (weighted avg): **0.98**

**Observation:**  
Achieved the **best overall performance**. Demonstrates strong separation between phishing and legitimate emails when combined with TF-IDF features.

---

### Decision Tree
- Accuracy: **97.22%**
- Precision (weighted avg): **0.97**
- Recall (weighted avg): **0.97**
- F1-score (weighted avg): **0.97**

**Observation:**  
Good performance but more prone to overfitting compared to linear models.

---

## Best Model Selection
The **Support Vector Machine (SVM)** was selected as the best-performing model due to:
- Highest accuracy
- Strong precision and recall balance
- Lower false-negative rate for phishing detection

---

## SOC-Relevant Analysis

- **High recall** is critical to minimize missed phishing emails that could lead to credential compromise.
- **False positives**, while present, are acceptable in SOC environments where security is prioritized over convenience.
- Text-based detection is effective but should be complemented with:
  - URL analysis
  - Email header inspection
  - Attachment behavior analysis

---

## Limitations
- Only email body text was analyzed
- No sender reputation or header metadata
- Dataset may not reflect highly targeted spear-phishing attacks

---

## Future Improvements
- Incorporate URL and domain-based features
- Add email header analysis (SPF, DKIM, DMARC)
- Test transformer-based NLP models (e.g., BERT)
- Integrate with SIEM/SOAR simulation workflows

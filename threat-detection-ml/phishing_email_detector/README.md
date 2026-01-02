# Phishing Email Detector

## Overview
This project implements a machine-learning–based phishing email detector that identifies malicious emails by analyzing their textual content. The goal is to demonstrate how automated phishing detection can support Security Operations Center (SOC) workflows by assisting analysts in identifying social engineering threats at scale.

---

## Problem Statement
Phishing remains one of the most common initial access vectors in cyberattacks. As email volumes grow, manual inspection becomes impractical, creating the need for automated detection mechanisms that can flag potentially malicious messages for further investigation.

---

## Detection Approach
- **Detection Type:** Binary classification (Phishing vs Legitimate)
- **Learning Paradigm:** Supervised machine learning
- **Feature Extraction:** TF-IDF vectorization of email text
- **Focus:** Detecting phishing characteristics within email body content

The detector is designed to reflect a simplified version of real-world phishing detection pipelines used in SOC environments.

---

## Dataset
Data from kaggle was taken in account.
- Email dataset containing phishing (spam) and legitimate (ham) messages
- Labeled data used for supervised learning
- Preprocessing steps include text cleaning and normalization
- Data is split into training and testing sets

---

## Models Used
The following machine learning models were implemented and evaluated:
- Logistic Regression
- Multinomial Naive Bayes
- Support Vector Machine (SVM)
- Decision Tree

Model training, evaluation, and comparisons are documented in the analysis notebook.

---

## Evaluation
Model evaluation metrics, comparisons, and SOC-oriented analysis are documented separately in  
[`results.md`](./results.md).

---

## Disclaimer
This project is intended for educational and portfolio purposes only and is not designed for production deployment.

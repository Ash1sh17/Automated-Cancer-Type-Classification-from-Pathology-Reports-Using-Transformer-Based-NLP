# Automated Cancer Type Classification from Pathology Reports Using Transformer-Based NLP

## Project Description
This project evaluates traditional machine learning models and state-of-the-art transformer-based NLP architectures (Google BERT and PubMedBERT) to automate the classification of cancer types directly from unstructured textual clinical pathology reports.

---

## Dataset Distribution
The dataset exhibits a class imbalance across various cancer types, with Breast Invasive Carcinoma (BRCA) representing the largest volume of clinical text records.

![Dataset Distribution](cancer types.png)
*Figure 1: Total number of pathology reports processed per unique cancer type.*

---

## How to Run the Code

### 1. Installation
Install the necessary modeling and evaluation dependencies using your terminal:
```bash
pip install torch transformers pandas scikit-learn matplotlib seaborn

# NeuroLogic '26 Datathon — NLP Solutions

**Author:** Kishan Kumar
**GitHub:** https://github.com/techwithkishan/Neuro-Logic26-Datathon
**Event:** NeuroLogic '26 Datathon, GGITS — April 25, 2026

---

## 🏆 Results Summary

| Challenge | Task | Metric | Score |
|---|---|---|---|
| Challenge 1 | Disaster Tweet Classification | Macro F1 | **0.8955** |
| Challenge 2 | Fake News Detection | Accuracy | **99.87%** |
| Challenge 3 | Multilingual Toxic Comments | ROC-AUC | **0.9922** |

---

## 🚨 Challenge 1 — Disaster Tweet Classification

**Model:** `vinai/bertweet-base` — pretrained on 850M tweets
**Dataset:** 25,933 train / 2,000 test
**Labels:** `Informative` / `Not Informative`

**Approach:**
- Combined Tweet Text + Information Source + Information Type
- Fine-tuned BERTweet for 3 epochs
- 90/10 train-validation split, seed=42
- max_length=128, batch_size=32, fp16=True

**Validation Results:**

| Class | Precision | Recall | F1 |
|---|---|---|---|
| Informative | 0.92 | 0.93 | 0.92 |
| Not Informative | 0.87 | 0.86 | 0.87 |
| **Macro F1** | | | **0.8955** |

---

## 📰 Challenge 2 — Fake News Detection

**Model:** `roberta-base`
**Dataset:** 18,176 train / 1,541 test
**Labels:** `True` / `False`

**Approach:**
- Combined title + [SEP] + text + [SEP] + subject
- Fine-tuned RoBERTa for 3 epochs
- 90/10 train-validation split, seed=42
- max_length=256, batch_size=16, fp16=True

**Validation Results:**

| Class | Precision | Recall | F1 |
|---|---|---|---|
| False | 1.00 | 1.00 | 1.00 |
| True | 1.00 | 1.00 | 1.00 |
| **Accuracy** | | | **99.87%** |

---

## 🌐 Challenge 3 — Multilingual Toxic Comment Classification

**Model:** `xlm-roberta-base` — supports 100 languages
**Dataset:** 9,000 train / 1,000 test
**Labels:** `0` (Non-Toxic) / `1` (Toxic)
**Languages:** Hindi + English

**Approach:**
- Fine-tuned XLM-RoBERTa for 3 epochs
- 90/10 train-validation split, seed=42
- max_length=128, batch_size=16, fp16=True
- ROC-AUC computed using softmax probabilities

**Validation Results:**

| Class | Precision | Recall | F1 |
|---|---|---|---|
| Non-Toxic (0) | 0.97 | 0.96 | 0.96 |
| Toxic (1) | 0.96 | 0.97 | 0.96 |
| **ROC-AUC** | | | **0.9922** |

---

## ▶️ How to Reproduce

1. Open Google Colab — enable T4 GPU (Runtime → Change runtime type → T4 GPU)
2. Upload dataset files to Colab
3. Install dependencies: `pip install -r requirements.txt`
4. Run notebooks top to bottom:
   - `challenge1/C1_Disaster_Tweets.ipynb`
   - `challenge2/C2_Fake_News.ipynb`
   - `challenge3/C3_Toxic_Comments.ipynb`
5. Prediction files will be saved automatically

> All random seeds set to 42 for reproducibility

---

## 📁 Repository Structure

- 📁 challenge1/
  - NL'26_Datathon_Challenge_1.ipynb
  - Disaster_no_label.csv
- 📁 challenge2/
  - NL'26_Datathon_Challenge_2.ipynb
  - FakeNews_no_labels.csv
- 📁 challenge3/
  - NL'26_Datathon_Challenge_3.ipynb
  - toxic_no_label_evaluation.xlsx
- 📁 screenshots/
  - c1_results.png
  - c2_results.png
  - c3_results.png
- README.md
- requirements.txt
---

## 🛠️ Technology Stack

- Python 3.12
- HuggingFace Transformers
- PyTorch
- scikit-learn
- Google Colab T4 GPU
- pandas, numpy, openpyxl

---

## 📊 Dataset Usage

- Official datasets provided by NeuroLogic '26 organizers
- Training: `with_label` files used for model training
- Evaluation: `no_label` files used for predictions
- Evaluation method: 90/10 train-validation split, seed=42

---

## ✅ Pre-trained Models

| Model | Challenge | License |
|---|---|---|
| `vinai/bertweet-base` | Challenge 1 | MIT |
| `roberta-base` | Challenge 2 | MIT |
| `xlm-roberta-base` | Challenge 3 | MIT |

All models publicly available on HuggingFace Hub.
Use of pre-trained models explicitly permitted per NeuroLogic '26 rules.

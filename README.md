================================================================
NEUROLOGIC '26 DATATHON — NLP SOLUTIONS
================================================================
Author     : Kishan Kumar
GitHub     : https://github.com/techwithkishan/neurologic26-datathon](https://github.com/techwithkishan/Neuro-Logic26-Datathon
Event      : NeuroLogic '26 Datathon, GGITS — April 25, 2026
Deadline   : 10:00 PM IST, April 25, 2026
================================================================

----------------------------------------------------------------
RESULTS SUMMARY
----------------------------------------------------------------
Challenge 1 | Disaster Tweet Classification | Macro F1   : 0.8955
Challenge 2 | Fake News Detection           | Accuracy   : 99.87%
Challenge 3 | Multilingual Toxic Comments   | ROC-AUC    : 0.9922
----------------------------------------------------------------

================================================================
CHALLENGE 1 — DISASTER TWEET CLASSIFICATION
================================================================

TASK:
Binary classification of tweets as Informative or Not Informative
during disaster events.

DATASET:
- Training : Disaster_with_label.csv (25,933 rows)
- Evaluation: Disaster_no_label.csv  (2,000 rows)
- Labels   : Informative / Not Informative

MODEL:
vinai/bertweet-base — pretrained on 850 million tweets
Chosen for its domain-specific pretraining on Twitter data,
making it superior to generic BERT for social media text.

APPROACH:
1. Combined Tweet Text + Information Source + Information Type
   into a single text feature for richer signal
2. Fine-tuned BERTweet for 3 epochs
3. 90/10 train-validation split (seed=42)
4. max_length=128, batch_size=32, fp16=True

VALIDATION RESULTS:
                 precision  recall  f1-score  support
Informative         0.92    0.93      0.92     1647
Not Informative     0.87    0.86      0.87      947
accuracy                              0.90     2594
macro avg           0.90    0.90      0.90     2594

Macro F1-Score : 0.8955

REAL-WORLD IMPACT:
Enables first responders to rapidly identify actionable disaster
information from social media during emergencies.

================================================================
CHALLENGE 2 — FAKE NEWS DETECTION
================================================================

TASK:
Binary classification of news articles as True (reliable)
or False (fake/misleading).

DATASET:
- Training : fakenews_with_labels.csv (18,176 rows)
- Evaluation: FakeNews_no_labels.csv  (1,541 rows)
- Labels   : True / False
- Encoding : latin-1

MODEL:
roberta-base — Robustly Optimized BERT Pretraining Approach
Chosen for its superior performance on binary text classification.

APPROACH:
1. Combined title + [SEP] + text + [SEP] + subject columns
   to capture full article context
2. Fine-tuned RoBERTa for 3 epochs
3. 90/10 train-validation split (seed=42)
4. max_length=256, batch_size=16, fp16=True

VALIDATION RESULTS:
          precision  recall  f1-score  support
False        1.00    1.00      1.00      332
True         1.00    1.00      1.00      455
accuracy                       1.00      787

Accuracy : 99.87%

REAL-WORLD IMPACT:
Automated misinformation detection to maintain trust in
digital information ecosystems at scale.

================================================================
CHALLENGE 3 — MULTILINGUAL TOXIC COMMENT CLASSIFICATION
================================================================

TASK:
Binary classification of multilingual comments as Toxic (1)
or Non-Toxic (0) across Hindi and English text.

DATASET:
- Training : toxic_labeled.xlsx        (9,000 rows)
- Evaluation: toxic_no_label_evaluation.xlsx (1,000 rows)
- Labels   : 0 (Non-Toxic) / 1 (Toxic)
- Languages: Hindi + English (multilingual)

MODEL:
xlm-roberta-base — Cross-lingual RoBERTa
Chosen for its native support of 100 languages, making it
ideal for multilingual toxic content detection.

APPROACH:
1. Loaded Excel files using openpyxl
2. Dropped null text rows (4 rows)
3. Fine-tuned XLM-RoBERTa for 3 epochs
4. 90/10 train-validation split (seed=42)
5. max_length=128, batch_size=16, fp16=True
6. ROC-AUC computed using softmax probabilities

VALIDATION RESULTS:
               precision  recall  f1-score  support
Non-Toxic (0)     0.97    0.96      0.96      444
Toxic (1)         0.96    0.97      0.96      456
accuracy                            0.96      900

ROC-AUC Score : 0.9922

REAL-WORLD IMPACT:
Scalable multilingual content moderation for global platforms
handling diverse languages and cultural contexts.

================================================================
HOW TO REPRODUCE RESULTS
================================================================

ENVIRONMENT:
- Platform : Google Colab (T4 GPU recommended)
- Python   : 3.12

STEP 1 — Install dependencies:
pip install -r requirements.txt

STEP 2 — Upload dataset files to Colab:
Challenge 1 : Disaster_with_label.csv, Disaster_no_label.csv
Challenge 2 : fakenews_with_labels.csv, FakeNews_no_labels.csv
Challenge 3 : toxic_labeled.xlsx, toxic_no_label_evaluation.xlsx

STEP 3 — Run notebooks in order (top to bottom):
Challenge 1 : challenge1/C1_Disaster_Tweets.ipynb
Challenge 2 : challenge2/C2_Fake_News.ipynb
Challenge 3 : challenge3/C3_Toxic_Comments.ipynb

STEP 4 — Output files:
Challenge 1 : Disaster_no_label.csv       (filled predictions)
Challenge 2 : FakeNews_no_labels.csv      (filled predictions)
Challenge 3 : toxic_no_label_evaluation.xlsx (filled predictions)

NOTES:
- All random seeds set to 42 for reproducibility
- Enable T4 GPU: Runtime → Change runtime type → T4 GPU
- Run all cells top to bottom without skipping

================================================================
DATASET USAGE
================================================================
- Official datasets provided by NeuroLogic '26 organizers
- Training: with_label files used for model training
- Evaluation: no_label files used for generating predictions
- Labels predicted exactly match original label format

================================================================
EVALUATION METHOD
================================================================
- Train-Validation Split: 90% train / 10% validation
- Random seed: 42 (for reproducibility)
- Challenge 1: Macro F1-Score
- Challenge 2: Overall Accuracy
- Challenge 3: Mean ROC-AUC Score

================================================================
TECHNOLOGY STACK
================================================================
- Python 3.12
- HuggingFace Transformers
- PyTorch
- scikit-learn
- pandas, numpy
- Google Colab T4 GPU
- openpyxl (Excel file handling)

================================================================
PRE-TRAINED MODELS USED
================================================================
- vinai/bertweet-base  (Challenge 1) — MIT License
- roberta-base         (Challenge 2) — MIT License
- xlm-roberta-base     (Challenge 3) — MIT License

All models are publicly available on HuggingFace Hub.
Use of pre-trained models is explicitly permitted as per
NeuroLogic '26 Datathon official rules.

================================================================

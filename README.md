# DSC232R: Assessing Bias in Amazon Vine Reviews

## Group Members
- Jenna Brooks ([j8brooks@ucsd.edu](mailto:j8brooks@ucsd.edu))
- JoJo Lin ([jol145@ucsd.edu](mailto:jol145@ucsd.edu))
- Caroline Porche ([cporche@ucsd.edu](mailto:cporche@ucsd.edu))
- Matthew Takeuchi ([m1takeuc@ucsd.edu](mailto:m1takeuc@ucsd.edu))

---

## I. Introduction

Amazon Vine is an invite-only program where top reviewers receive free products in exchange for writing reviews. While marketed as unbiased, past research suggests such incentives may affect the tone and content of reviews.

This project investigates whether Vine reviews differ significantly from non-Vine reviews in terms of:
- Star ratings
- Helpfulness scores
- Sentiment polarity
- Review length

We use a cleaned subset of the [Amazon US Customer Reviews Dataset](https://www.kaggle.com/datasets/cynthiarempel/amazon-us-customer-reviews-dataset), and apply classification models (logistic regression, Naive Bayes, Random Forest) to explore potential bias in Vine reviews.

---

## II. Figures Summary

- **Rating Distribution:** 5-star reviews dominate (63.91%), indicating strong class imbalance.
- **Vine vs. Non-Vine Ratings:** Vine reviews are more evenly spread across star ratings.
- **Helpfulness:** Vine reviews have higher average helpfulness scores.
- **Sentiment Polarity:** Vine reviews show narrower sentiment distribution than non-Vine.
- **Product Categories:** Sentiment varies by category, with Digital Music most positive and Gift Cards least.

---

## III. Methods

- Selected 9 categories for analysis (e.g., Beauty, Electronics, Gift Cards).
- Cleaned 20M+ records down to ~193K (0.41% Vine).
- Preprocessing included:
  - Removal of missing values & duplicates
  - TF-IDF vectorization of text
  - Feature engineering (review length, sentiment polarity)
- Models used:
  - Logistic Regression (final)
  - Naive Bayes
  - Random Forest
- Tools:
  - PySpark, MLlib, Google Colab, SDSC
  - matplotlib, seaborn, pandas, NumPy

---

## IV. Results

- **Final Model:** Logistic Regression
- **Test Accuracy:** 67.4%
- **F1 Score:** 0.5983
- Vine reviews: longer, more helpful, more moderate in tone
- Non-Vine reviews: more emotionally extreme, more skewed toward 5 stars

---

## V. Discussion

- Model performance impacted by class imbalance
- Stratified sampling or class weighting could improve results
- Resource limitations (runtime, SDSC access) constrained deeper exploration
- Star ratings don’t always align with textual sentiment
- Ethical considerations: review privacy, category selection, ID anonymization

---

## VI. Conclusion

Vine reviews show distinct patterns: they’re more moderate, more helpful, and longer. Despite being incentivized, they may offer higher-quality feedback. Our model performed reasonably well, though limited by dataset imbalance and computational constraints. Future work could integrate sentiment directly and explore more advanced NLP models.

---

## VII. Statement of Collaboration

**Jenna**  
**Title:** Data Exploration & Introduction Writer  
**Contribution:** Initiated the project and contributed to idea development, located the Kaggle dataset, performed initial data exploration and visualizations, wrote the Introduction and Figures sections, and updated the project README.

**Matt**  
**Title:** Modeling Lead & Data Engineer  
**Contribution:** Led model fitting and evaluation processes and provided access to SDSC resources for computing, performed data cleaning and preprocessing.

**Caroline**  
**Title:** Project Manager & Data Engineer  
**Contribution:** Managed the project timeline and deadlines, set up Kaggle API and Google Colab environments, performed data cleaning and preprocessing, wrote the Methods section, and organized the GitHub repository including the README documentation.

**Jojo**  
**Title:** Results Analyst & Visualization Developer  
**Contribution:** Created visualizations in code to support analysis, authored the Results and Conclusions sections, and contributed to interpretation of model performance.

---

## VIII. Final Deliverables

- 📄 [Final Report (Google Doc)](https://docs.google.com/document/d/19uSUlNqZAf24s00qddqhPWhanOm71eJqbT_h4E8t81s/edit?usp=sharing)  
- 📓 [Final Colab Notebook](https://colab.research.google.com/drive/1r6Rg66iP_PTqvRSvZetj451lW5J-B0wm?usp=sharing)  
- 📓 [Milestone 3 Notebook](https://colab.research.google.com/drive/1B87bLoxxEpuh9BflsjAw8hpDD89787tK?usp=sharing)  
- 📓 [Milestone 2 Notebook](https://colab.research.google.com/drive/1qLS9L-2DxKVYe4vZ5wNhfQAtpAgXWI1d?usp=sharing)

---

## IX. Environment Setup (Colab)

### Kaggle API Setup
```python
from google.colab import files
files.upload()

!mkdir -p ~/.kaggle
!cp kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json



!pip install kaggle
!pip install nltk
Note: We use the Kaggle API (`!kaggle datasets download`) instead of `!wget` because the Amazon review dataset requires authentication via a Kaggle API key. This is functionally equivalent to `wget` but secure.
```

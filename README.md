# DSC232R: Assessing Bias in Amazon Vine Reviews

## Group Members
- Jenna Brooks ([j8brooks@ucsd.edu](mailto:j8brooks@ucsd.edu))
- JoJo Lin ([jol145@ucsd.edu](mailto:jol145@ucsd.edu))
- Caroline Porche ([cporche@ucsd.edu](mailto:cporche@ucsd.edu))
- Matthew Takeuchi ([m1takeuc@ucsd.edu](mailto:m1takeuc@ucsd.edu))

---

## I. Introduction

Amazon Vine is an invite-only program where top reviewers receive free products in exchange for writing reviews. While marketed as unbiased, past research suggests such incentives may affect tone and content.

This project investigates whether Vine reviews differ from non-Vine reviews by:
- Comparing characteristics like length, helpfulness, and sentiment
- Predicting star ratings using review text and metadata
- Evaluating model performance using logistic regression and other classifiers

We use the [Amazon US Customer Reviews Dataset](https://www.kaggle.com/datasets/cynthiarempel/amazon-us-customer-reviews-dataset) and build models in PySpark within Google Colab.

---

## II. Figures Summary

- **Rating Distribution:** 5-star reviews dominate (63.91%)
- **Vine vs. Non-Vine Ratings:** Vine reviews are more evenly distributed
- **Helpfulness:** Vine reviews scored higher on average helpfulness
- **Sentiment:** Vine reviews showed narrower, more moderate sentiment range

---

## III. Methods

- Focused on 9 product categories
- Cleaned and filtered down to 193,085 reviews (~0.41% Vine)
- Preprocessing:
  - Removed nulls and duplicates
  - Tokenized, cleaned text
  - TF-IDF vectorization
  - Feature engineering: review length, sentiment polarity
- Models used:
  - Logistic Regression (final)
  - Naive Bayes
  - Random Forest
- All modeling and preprocessing in PySpark (MLlib) on Google Colab with SDSC

---

## IV. Results

- Final Model: Logistic Regression  
- Accuracy: 67.4%  
- F1 Score: 0.5983  
- Vine reviews had longer text, higher helpfulness, and more moderate tone
- Non-Vine reviews were shorter and more emotionally polarized
- Vine reviews received slightly more verified purchase flags

---

## V. Discussion

- Performance limited by star rating imbalance (5-stars = 64% of all reviews)
- Stratified sampling could have improved class representation
- SDSC resources significantly improved runtime (30 mins vs several hours)
- Ethical decisions included:
  - Avoiding user ID tracking
  - Minimizing reading of sensitive reviews
  - Excluding potentially sensitive product categories

---

## VI. Conclusion

Vine reviews differ in tone, length, and helpfulness, possibly due to expectations set by the program. Our results suggest these reviews may actually be more critical and informative than typical non-Vine ones.

While model performance was moderate, limitations around data imbalance and textual ambiguity were expected. Future directions include using sentiment as a feature, incorporating embeddings, and modeling helpfulness directly.

---

## VII. Statement of Collaboration

**Jenna**  
Title: Data Exploration & Introduction Writer  
Contribution: Project idea generation, found dataset, initial data exploration, visualizations, Introduction and Figures sections, updated README.

**Matt**  
Title: Modeling Lead & Data Engineer  
Contribution: Led model development and evaluation, provided SDSC access, assisted with data processing.

**Caroline**  
Title: Project Manager & Data Engineer  
Contribution: Managed timeline and coordination, set up Kaggle API and Colab, conducted data cleaning, wrote Methods section, organized GitHub and README.

**JoJo**  
Title: Results Analyst & Visualization Developer  
Contribution: Wrote Results and Conclusion sections, created performance visualizations, supported model interpretation.

---

## VIII. Final Deliverables

- Final Colab Notebook: [Link](https://colab.research.google.com/drive/1r6Rg66iP_PTqvRSvZetj451lW5J-B0wm?usp=sharing)  
- Final Written Report: [Link](https://docs.google.com/document/d/19uSUlNqZAf24s00qddqhPWhanOm71eJqbT_h4E8t81s/edit?usp=sharing)  
- Milestone 3 Notebook: [Link](https://colab.research.google.com/drive/1B87bLoxxEpuh9BflsjAw8hpDD89787tK?usp=sharing)  
- Milestone 2 Notebook: [Link](https://colab.research.google.com/drive/1qLS9L-2DxKVYe4vZ5wNhfQAtpAgXWI1d?usp=sharing)

---

## IX. Environment Setup (Google Colab)

```python
from google.colab import files
files.upload()

!mkdir -p ~/.kaggle
!cp kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json

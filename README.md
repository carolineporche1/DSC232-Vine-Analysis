# DSC232R Vine Review Analysis

## Group Members
- Jenna Brooks ([j8brooks@ucsd.edu](mailto:j8brooks@ucsd.edu))
- JoJo Lin ([jol145@ucsd.edu](mailto:jol145@ucsd.edu))
- Caroline Porche ([cporche@ucsd.edu](mailto:cporche@ucsd.edu))
- Matthew Takeuchi ([m1takeuc@ucsd.edu](mailto:m1takeuc@ucsd.edu))

## Dataset
[Amazon US Customer Reviews Dataset (Kaggle)](https://www.kaggle.com/datasets/cynthiarempel/amazon-us-customer-reviews-dataset)

This dataset includes millions of Amazon customer reviews across a wide range of product categories. It contains fields such as star ratings, review text, helpfulness votes, verification status, and whether the review was part of Amazon’s Vine program.

## Project Objective
This project investigates the Amazon Vine program, where reviewers receive free products in exchange for writing reviews. We aim to:

- Analyze the impact of Vine reviews on overall product ratings.
- Identify differences between Vine and non-Vine reviews:
  - Rating distributions
  - Review length
  - Helpfulness scores
  - Sentiment polarity
  - Verified purchase frequency
- Explore category-level differences in Vine influence.
- Evaluate review authenticity and marketing effectiveness.

---

## Milestone 3: Preprocessing, Modeling & Evaluation

### Updated Notebook
[Milestone 3 Colab Notebook](https://colab.research.google.com/drive/1B87bLoxxEpuh9BflsjAw8hpDD89787tK?usp=sharing)

### Preprocessing Summary
We completed full preprocessing, including:

- Imputation for missing values in review text and helpful votes
- Feature scaling using `MinMaxScaler` and `StandardScaler`
- Text cleaning: tokenization, lemmatization, lowercasing, punctuation removal
- Sentiment score extraction using Spark NLP
- Feature engineering:
  - Review length (word/character count)
  - Log-transformed helpfulness scores
  - Interaction terms (e.g., `vine * verified_purchase`)
  - One-hot and label encoding of categorical variables

---

### First Model: Logistic Regression
We trained a logistic regression model to classify Vine vs. non-Vine reviews.

#### Evaluation Metrics
- **Training Accuracy**: 76.4%
- **Validation Accuracy**: 74.8%
- **Test Accuracy**: 74.9%
- **F1 Score (Test)**: 0.71

#### Underfitting or Overfitting?
- Training and validation/test accuracy are closely aligned.
- **Conclusion**: Slight underfitting — model may benefit from increased complexity (e.g., decision trees, ensembles).

#### Ground Truth vs. Predictions
Example output:

!pip install kaggle
!pip install nltk
Note: We use the Kaggle API (`!kaggle datasets download`) instead of `!wget` because the Amazon review dataset requires authentication via a Kaggle API key. This is functionally equivalent to `wget` but secure.
```

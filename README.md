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
- Identify key differences between Vine and non-Vine reviews, including:
  - Rating distributions
  - Review length
  - Helpfulness scores
  - Sentiment polarity
  - Verified purchase frequency
- Determine if certain product categories are more influenced by Vine participation.
- Evaluate the perceived authenticity and effectiveness of Vine reviews from consumer and seller perspectives.

## Notebook

View and run our full project notebook in Google Colab:

[Open in Google Colab](https://colab.research.google.com/drive/1qLS9L-2DxKVYe4vZ5wNhfQAtpAgXWI1d?usp=sharing)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1qLS9L-2DxKVYe4vZ5wNhfQAtpAgXWI1d?usp=sharing)

## Data Exploration

Our exploration focused on understanding the structure and contents of the dataset:

- Total number of records and features
- Distribution of:
  - `star_rating`
  - `review_length` (character count)
  - `helpful_votes`
- Presence of missing values
- Variable types:
  - `star_rating`: ordinal
  - `helpful_votes`, `total_votes`: ratio
  - `review_length`: interval
  - `vine`, `verified_purchase`: nominal (binary)

We visualized rating and review differences between Vine and non-Vine reviewers using:

- Histograms and bar plots
- Scatter plots showing relationship between length and helpfulness
- Category-level aggregations

## Data Preprocessing Plan

We prepared the data with the following steps:

- Dropped entries with missing values in key columns
- Cleaned review text (lowercased, removed punctuation, tokenized)
- Converted categorical variables (`vine`, `verified_purchase`) into binary indicators
- Handled class imbalance where necessary
- Conducted sentiment analysis using Spark NLP and NLTK tools

## Environment Setup (Colab Instructions)

## Kaggle API Setup

To use the Kaggle API in Google Colab:

1. Go to your [Kaggle Account Settings](https://www.kaggle.com/account) and click **"Create New API Token"**.
2. This will download a file called `kaggle.json`.

3. In Colab, upload it with the following code block:

```python
from google.colab import files
files.upload()  # Upload kaggle.json

!mkdir -p ~/.kaggle
!cp kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json




To run our notebook on Google Colab, install required packages:

```python
!pip install pyspark
!pip install kaggle
!pip install nltk
Note: We use the Kaggle API (`!kaggle datasets download`) instead of `!wget` because the Amazon review dataset requires authentication via a Kaggle API key. This is functionally equivalent to `wget` but secure.


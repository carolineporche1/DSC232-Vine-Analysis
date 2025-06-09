# DSC232R: Assessing Bias in Amazon Vine Reviews

## Group Members
- Jenna Brooks ([j8brooks@ucsd.edu](mailto:j8brooks@ucsd.edu))
- JoJo Lin ([jol145@ucsd.edu](mailto:jol145@ucsd.edu))
- Caroline Porche ([cporche@ucsd.edu](mailto:cporche@ucsd.edu))
- Matthew Takeuchi ([m1takeuc@ucsd.edu](mailto:m1takeuc@ucsd.edu))

---

## I. Introduction

Amazon Vine is an invite-only review program that selects highest-quality contributors in Amazon’s review community to serve as Vine Voices. Vine Voices receive free items in exchange for writing reviews, a program that sellers use to boost visibility and credibility of products (Amazon.com, Inc., n.d.). While Amazon claims that Vine reviews “reflect [reviewers’] honest and unbiased opinions — positive, neutral, or negative,” previous research suggests that enrollment in such programs can change the semantics reviewers use, thereby influencing product reviews (Amazon.com, Inc., n.d.; Puranam & Cardie, 2014).

This study evaluates whether there is a significant difference between Vine and non-Vine reviews on product star ratings to assess the Vine program’s impact on review bias.

We use data from the Amazon Customer Reviews Dataset from Kaggle, which contains over 6 million Amazon customer product reviews across multiple product categories over two decades. It offers detailed insights into customer experiences, product ratings, review text, helpfulness votes, and verified purchases (Rempel, n.d.).

We seek to understand whether there is bias in Vine program reviews compared to non-Vine reviews. We hypothesize that Vine reviews are more likely to have higher ratings than non-Vine reviews. Using logistic regression, we aim to predict the star rating of products based on review text and length.

By analyzing differences in product ratings between Vine and non-Vine reviews, this study assesses whether Amazon’s paid-review program introduces bias, offering critical insights into how incentivized reviews shape consumer perceptions and trust in online platforms. Results can assist consumers in making informed purchasing decisions and offer sellers a better understanding of how review programs influence brand perception and sales performance.

We used data from the [Amazon US Customer Reviews Dataset](https://www.kaggle.com/datasets/cynthiarempel/amazon-us-customer-reviews-dataset), applying classification models (logistic regression, Naive Bayes, and Random Forest) to explore review bias.

---

## II. Figures

- **Figure 1:** Over 63% of all reviews are 5-star, indicating class imbalance.
- **Figure 2:** Non-Vine reviews skew more positive than Vine reviews, which are more evenly distributed.
- **Figure 3:** Vine reviews have significantly higher average helpfulness scores.
- **Figure 4:** Sentiment polarity varies by product category (e.g., Digital Music highest, Gift Cards lowest).
- **Figure 5:** Non-Vine reviews show more emotional variability in sentiment; Vine reviews are more moderate.

---

## III. Methods

### Data Exploration  
We selected data from nine diverse Amazon product categories: Beauty, Automotive, Digital Music Purchase, Outdoors, Baby, Electronics, Gift Cards, Furniture, and Tools. Each category was reviewed for data volume, Vine label distribution, star rating distribution, and the presence of missing values. Vine reviews represented approximately 0.41% of the dataset, indicating a significant class imbalance.

### Preprocessing  
To enable efficient processing in Google Colab, the dataset was partitioned into eight chunks. We removed reviews containing null values in either the `review_body` or `star_rating` fields and eliminated duplicates using the `review_id`. We filtered to include only clearly labeled Vine (“Y”) and Non-Vine (“N”) reviews. From the cleaned data, we selected the following features for modeling:
- `review_id`
- `star_rating`
- `review_body`

Additional preprocessing steps included:
- Binarizing `star_rating`: ratings ≥ 4 labeled as 1 (positive), ratings < 4 as 0 (negative)
- Engineering a `review_length` feature (word count of `review_body`)
- Text processing using the following Spark MLlib pipeline:  

### Model 1: Naive Bayes  
We trained a Multinomial Naive Bayes classifier using TF-IDF features and `review_length`. The model was configured using:
```python
NaiveBayes(modelType="multinomial", featuresCol="features", labelCol="label")
```
### Model 2: Logistic Regression
A logistic regression model was trained on the same features. It was configured with:
```python
LogisticRegression(featuresCol="features", labelCol="label", maxIter=20, regParam=0.1)
```
### Model 3: Random Forest Classifier
A random forest model was trained on the same feature set. he model was evaluated using the same metrics: accuracy, precision, recall, and F1-score.

 Configuration:
 ```python
RandomForestClassifier(labelCol="label", featuresCol="features", numTrees=100, maxDepth=5)
 ```
### Tools and Environment 
All data processing and modeling were conducted using PySpark within Google Colab, with compute support from the San Diego Supercomputer Center (SDSC). We used Spark MLlib for feature engineering and modeling. Visualizations and exploratory data analysis were performed with matplotlib and seaborn, and pandas and NumPy were used for tabular operations and summary statistics.

---

## IV. Results

- **Final Model:** Logistic Regression  
- **Accuracy:** 67.4%  
- **F1 Score:** 0.5983  

**Insights:**
- 5-star reviews dominate the dataset (63.91%)
- Vine reviews are more balanced across ratings and have higher helpfulness scores
- Vine reviews are longer (average 1145 characters vs. 277 for non-Vine)
- Sentiment polarity in Vine reviews is more concentrated and less extreme
- Logistic regression outperformed tree-based models in consistency

---

## V. Discussion

While logistic regression achieved 67.4% accuracy and an F1 score of 0.5983, these metrics reflect the dataset's class imbalance. Even with sampling and feature engineering, models tended to predict the majority (5-star) class.

**Challenges:**
- Severe class imbalance and limited Vine data (only 0.41% of total)
- Run-time and memory constraints required SDSC resources
- Possible mismatch between review text and star ratings
- Lack of updated review tracking or sentiment alignment

**Ethical Considerations:**
- Avoided tracking user IDs
- Minimized reading of full reviews to protect privacy
- Focused on general product categories to avoid sensitive content

---

## VI. Conclusion

This project demonstrates measurable differences between Vine and non-Vine reviews. While Vine reviews are incentivized, they appear more thoughtful, moderate, and helpful on average. Our logistic regression model shows that basic textual and structural features can help classify review type, though limitations exist due to data imbalance and ambiguity.

Future work could:
- Include direct sentiment polarity as a feature
- Incorporate embeddings (e.g., Word2Vec, BERT)
- Explore helpfulness score prediction
- Use stratified sampling or advanced resampling methods

---

## VII. Statement of Collaboration

**Jenna**  
Title: Data Exploration & Introduction Writer  
Contribution: Initiated the project and contributed to idea development, located the Kaggle dataset, performed initial data exploration and visualizations, wrote the Introduction and Figures sections, and updated the project README.

**Matt**  
Title: Modeling Lead & Data Engineer  
Contribution: Led model fitting and evaluation processes, provided SDSC access, assisted with data cleaning and preprocessing.

**Caroline**  
Title: Project Manager & Data Engineer  
Contribution: Managed project timeline and deadlines, set up Kaggle API and Google Colab environments, performed data cleaning, wrote the Methods section, and organized the GitHub repository and README documentation.

**JoJo**  
Title: Results Analyst & Visualization Developer  
Contribution: Created visualizations in code to support analysis, authored the Results and Conclusions sections, and contributed to interpretation of model performance.

---

## VIII. Final Project Assets

- Final Written Report: [https://docs.google.com/document/d/19uSUlNqZAf24s00qddqhPWhanOm71eJqbT_h4E8t81s/edit?usp=sharing](https://docs.google.com/document/d/19uSUlNqZAf24s00qddqhPWhanOm71eJqbT_h4E8t81s/edit?usp=sharing)
- Final Colab Notebook: [https://colab.research.google.com/drive/1GdWyqy86LHoyqyTSWoFi5fP_voTnJnVQ?usp=sharing]([https://colab.research.google.com/drive/1GdWyqy86LHoyqyTSWoFi5fP_voTnJnVQ?usp=sharing](https://colab.research.google.com/drive/1Gy3cueDS3KWO0iS7zt06BhRJ2ZBW5lGf?usp=sharing)  
- Milestone 3 Notebook: [https://colab.research.google.com/drive/1B87bLoxxEpuh9BflsjAw8hpDD89787tK?usp=sharing](https://colab.research.google.com/drive/1B87bLoxxEpuh9BflsjAw8hpDD89787tK?usp=sharing)  
- Milestone 2 Notebook: [https://colab.research.google.com/drive/1qLS9L-2DxKVYe4vZ5wNhfQAtpAgXWI1d?usp=sharing](https://colab.research.google.com/drive/1qLS9L-2DxKVYe4vZ5wNhfQAtpAgXWI1d?usp=sharing)  



---

## IX. Environment Setup (Google Colab)

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
```


## To run our notebook on Google Colab, install required packages:

```python
!pip install pyspark
!pip install kaggle
!pip install nltk
Note: We use the Kaggle API (`!kaggle datasets download`) instead of `!wget` because the Amazon review dataset requires authentication via a Kaggle API key. This is functionally equivalent to `wget` but secure.
```

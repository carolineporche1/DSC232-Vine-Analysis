# DSC232R: Assessing Bias in Amazon Vine Reviews

## Group Members
- Jenna Brooks ([j8brooks@ucsd.edu](mailto:j8brooks@ucsd.edu))
- JoJo Lin ([jol145@ucsd.edu](mailto:jol145@ucsd.edu))
- Caroline Porche ([cporche@ucsd.edu](mailto:cporche@ucsd.edu))
- Matthew Takeuchi ([m1takeuc@ucsd.edu](mailto:m1takeuc@ucsd.edu))

---

## Project Summary

Amazon Vine is a program where selected users receive free products in exchange for writing reviews. This project investigates whether Vine reviews differ from non-Vine reviews and explores potential bias introduced by this incentive structure.

We use a subset of the [Amazon US Customer Reviews Dataset](https://www.kaggle.com/datasets/cynthiarempel/amazon-us-customer-reviews-dataset) to:
- Compare Vine and non-Vine review characteristics
- Predict star ratings using review text and metadata
- Evaluate classification performance using logistic regression and other models

---

## Final Results

- Final Model: Logistic Regression  
- Accuracy: 67.4%  
- F1 Score: 0.5983  

Key Findings:
- Vine reviews are longer, more helpful, and more moderate in tone
- Non-Vine reviews show higher polarity and are more likely to be 5 stars
- Logistic regression outperformed more complex models due to its interpretability and consistent performance

---

## Project Assets

- Final Colab Notebook: [Link](https://colab.research.google.com/drive/1B87bLoxxEpuh9BflsjAw8hpDD89787tK?usp=sharing)  
- Final Written Report: [Link](https://docs.google.com/document/d/19uSUlNqZAf24s00qddqhPWhanOm71eJqbT_h4E8t81s/edit?usp=sharing)  
- Milestone 2 Notebook: [Link](https://colab.research.google.com/drive/1qLS9L-2DxKVYe4vZ5wNhfQAtpAgXWI1d?usp=sharing)

---

## Environment Setup (Google Colab)

To access the dataset via Kaggle in Colab:

```python
from google.colab import files
files.upload()

!mkdir -p ~/.kaggle
!cp kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json


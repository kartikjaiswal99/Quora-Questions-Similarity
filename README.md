# Quora Question Pairs Duplicate Detection Model

## 1. Business Problem

### 1.1 Description
Quora is a platform for gaining and sharing knowledge, allowing users to ask questions and connect with others who provide unique insights and quality answers. With over 100 million monthly visitors, many users often ask similarly worded questions. This can lead to a frustrating experience for seekers trying to find the best answer and for writers who feel compelled to respond to multiple versions of the same question.

Quora values canonical questions, which enhance the experience for both seekers and writers, providing long-term value.

> Credits: Kaggle

### Problem Statement
Identify which questions on Quora are duplicates of questions that have already been asked. This prediction can be useful for instantly providing answers to previously addressed queries.

### 1.2 Sources/Useful Links
- Source: [Kaggle Competition](https://www.kaggle.com/c/quora-question-pairs)
  
#### Useful Links
- Discussions: [Kaggle Discussion](https://www.kaggle.com/anokas/data-analysis-xgboost-starter-0-35460-lb/comments)
- Kaggle Winning Solutions: [Dropbox Link](https://www.dropbox.com/sh/93968nfnrzh8bp5/AACZdtsApc1QSTQc7X0H3QZ5a?dl=0)
- Blog 1: [Identifying Duplicate Questions on Quora](https://towardsdatascience.com/identifying-duplicate-questions-on-quora-top-12-on-kaggle-4c1cf93f1c30)

### 1.3 Real World/Business Objectives and Constraints
- The cost of misclassification can be very high.
- The model should provide the probability that a pair of questions are duplicates, allowing for flexibility in choosing thresholds.
- There are no strict latency concerns.
- Interpretability is partially important.

## 2. Machine Learning Problem

### 2.1 Data

#### 2.1.1 Data Overview
- Data is stored in a file: `Train.csv`
- `Train.csv` contains 5 columns: `qid1`, `qid2`, `question1`, `question2`, `is_duplicate`
- Size of `Train.csv`: 60 MB
- Number of rows in `Train.csv`: 404,290

#### 2.1.2 Example Data Point
| id | qid1 | qid2 | question1 | question2 | is_duplicate |
|----|------|------|-----------|-----------|--------------|
| 0  | 1    | 2    | What is the step by step guide to invest in share market in india? | What is the step by step guide to invest in share market? | 0 |
| 1  | 3    | 4    | What is the story of Kohinoor (Koh-i-Noor) Diamond? | What would happen if the Indian government stole the Kohinoor (Koh-i-Noor) diamond back? | 0 |
| 7  | 15   | 16   | How can I be a good geologist? | What should I do to be a great geologist? | 1 |
| 11 | 23   | 24   | How do I read and find my YouTube comments? | How can I see all my Youtube comments? | 1 |

### 2.2 Mapping the Real World Problem to an ML Problem

#### 2.2.1 Type of Machine Learning Problem
This is a binary classification problem where we predict whether a given pair of questions are duplicates.

#### 2.2.2 Performance Metric
- Metrics:
  - Log-loss: [Logarithmic Loss](https://www.kaggle.com/wiki/LogarithmicLoss)
  - Binary Confusion Matrix

### 2.3 Train and Test Construction
We build train and test datasets by randomly splitting the data in a ratio of 70:30 or 80:20, as we have sufficient data points to work with.

## 3. Model Performance
The following table summarizes the log loss results for different models tested:

|        Model        | Test Log Loss |
|---------------------|---------------|
|        Random       |    0.87262    |
| Logistic Regression |    0.54474   |
|      Linear SVM     |    0.52734  |
|       XGBoost       |    0.37250 |

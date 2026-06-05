# 🎓 Student Habits & Academic Success — Predictive Modeling in R

![Language](https://img.shields.io/badge/Language-R-276DC3?style=flat-square&logo=r)
![Models](https://img.shields.io/badge/Models-8%20Classifiers-brightgreen?style=flat-square)
![CV](https://img.shields.io/badge/Validation-10--Fold%20CV-orange?style=flat-square)
![Dataset](https://img.shields.io/badge/Dataset-1%2C000%20Students-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-success?style=flat-square)

**Author:** Royalpriesthood Olola | UEC671 · **Date:** May 2025

---

## 📌 Overview

Can lifestyle habits predict whether a student passes or fails? This project answers that question by combining exploratory data analysis with eight machine learning classification models applied to a dataset of 1,000 students.

Variables include study time, sleep, mental health, social media use, diet quality, internet quality, part-time job status, parental education, and more. The outcome variable is a binary **pass/fail** label derived from final exam scores.

The goal is not just accuracy — it's interpretability. Which habits matter most? Which assumptions about student life hold up in the data?

---

## 🗂️ Dataset

- **Source:** Kaggle — Student Habits vs Academic Performance
- **Size:** 1,000 students · 16 variables · No missing values
- **Outcome:** `pass_fail` — binary label created from `exam_score` (≥ 70 = pass)
- **Note:** `exam_score` was removed before modeling to prevent data leakage

---

## 🛠️ Methodology

### Pipeline

```text
Raw Data → Preprocessing → EDA → Remove exam_score → Train/Test Split
→ 8 Models → Evaluation → Results Comparison
```

### Preprocessing
- Factor encoding for categorical variables
- Removed `student_id`
- Checked for missing values
- Created `pass_fail` outcome variable
- Removed `exam_score` before modeling to prevent data leakage

### Models Used
- Logistic Regression (Full)
- Logistic Regression (Stepwise)
- Decision Tree (Unpruned)
- Decision Tree (Pruned)
- Random Forest
- SVM Linear
- SVM Polynomial
- SVM Radial

### Evaluation Methods
- Confusion Matrix Heatmaps
- Actual vs Predicted Classification Plots
- Predicted Probability Plots
- 10-Fold Cross-Validation
- Accuracy, Sensitivity, Specificity, Kappa, Balanced Accuracy

---

## 📁 Project Structure

```text
├── Final_Project_Improved.Rmd
├── Project_Walkthrough.md
├── Proposal_Revised.md
├── student_habits_performance.csv
└── README.md
```

---

## ❓ Research Questions

1. How do study habits influence the likelihood of passing or failing?
2. Does mental health affect academic success?
3. How do part-time jobs impact academic performance?
4. How does attendance percentage relate to exam scores?
5. Can we reliably predict pass/fail from lifestyle data alone?

---

## 📊 EDA Highlights

| Question | Key Finding |
|---|---|
| Study Habits vs Performance | Students who passed mostly studied between 3–6 hours per day |
| Mental Health vs Performance | Students with higher mental health ratings were more likely to pass |
| Part-Time Jobs Impact | Part-time jobs had less impact on performance than expected |
| Attendance vs Exam Scores | Attendance alone was a weaker predictor than study habits |

---

## 🏆 Model Results

| Model | Accuracy | Sensitivity | Specificity | Kappa | Balanced Accuracy | CV Accuracy |
|---|---|---|---|---|---|---|
| GLM Full | 0.9298 | 0.9247 | 0.9346 | 0.8594 | 0.9296 | 0.8745 |
| GLM Stepwise | 0.9331 | 0.9315 | 0.9346 | 0.8661 | 0.9331 | 0.8902 |
| DT Unpruned | 0.8462 | 0.7945 | 0.8954 | 0.6915 | 0.8450 | 0.8017 |
| DT Pruned | 0.8361 | 0.8630 | 0.8105 | 0.6725 | 0.8367 | 0.7944 |
| Random Forest | 0.9030 | 0.8973 | 0.9085 | 0.8059 | 0.9029 | 0.8574 |
| SVM Linear | 0.9331 | 0.9315 | 0.9346 | 0.8661 | 0.9331 | 0.8788 |
| SVM Polynomial | 0.9130 | 0.8973 | 0.9281 | 0.8259 | 0.9127 | 0.7917 |
| SVM Radial | 0.9298 | 0.9178 | 0.9412 | 0.8594 | 0.9295 | 0.8658 |

### Best Performing Models
- GLM Stepwise and SVM Linear achieved the highest accuracy at **93.31%**
- GLM Stepwise achieved the highest CV Accuracy at **89.02%**
- Decision Trees performed the weakest overall
- Random Forest and SVM models remained highly stable across validation folds

---

## 🔍 Key Findings

- Study hours per day was the strongest predictor of academic success
- Mental health showed a meaningful relationship with pass/fail outcomes
- Attendance alone was not enough to predict performance accurately
- Stepwise logistic regression improved interpretability while maintaining strong accuracy
- Cross-validation provided more reliable model evaluation than a single train/test split

---

## ▶️ How to Run

1. Download the dataset
2. Place `student_habits_performance.csv` in the same folder as the `.Rmd` file
3. Open `Final_Project_Improved.Rmd` in RStudio
4. Install required packages
5. Knit the file to HTML

```r
install.packages(c(
  "dplyr", "ggplot2", "e1071", "corrplot", "caret", "kernlab",
  "visdat", "car", "PRROC", "rpart", "rpart.plot",
  "randomForest", "reshape2", "scales"
))
```

---

## 🧰 Skills Demonstrated

`R` · `RMarkdown` · `ggplot2` · `caret` · `Binary Classification` ·
`Logistic Regression` · `Stepwise Selection` · `Decision Trees` ·
`Random Forest` · `SVM` · `10-Fold Cross-Validation` ·
`EDA` · `Data Leakage Prevention`

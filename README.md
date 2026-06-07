# 🎓 Student Habits & Academic Success — Predictive Modeling

![Language](https://img.shields.io/badge/Language-R-276DC3?style=flat-square&logo=r)
![Models](https://img.shields.io/badge/Models-8%20Classifiers-brightgreen?style=flat-square)
![CV](https://img.shields.io/badge/Validation-10--Fold%20CV-orange?style=flat-square)
![Dataset](https://img.shields.io/badge/Dataset-1%2C000%20Students-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-success?style=flat-square)



---

## 📌 Overview

> Can lifestyle habits predict whether a student passes or fails? This project answers that question by combining exploratory data analysis with eight machine learning classification models applied to a dataset of 1,000 students.

> Variables include study time, sleep, mental health, social media use, diet quality, internet quality, part-time job status, parental education, and more. The outcome variable is a binary **pass/fail** label derived from final exam scores (threshold = 70).

> The goal is not just accuracy — it's interpretability. Which habits matter most? Which assumptions about student life hold up in the data?

---

## 🗂️ Dataset

- **Source:** [Kaggle — Student Habits vs Academic Performance](https://www.kaggle.com/datasets/jayaantanaath/student-habits-vs-academic-performance)
- **Size:** 1,000 students · 16 variables · No missing values
- **Outcome:** `pass_fail` — binary label created from `exam_score` (≥ 70 = pass), then `exam_score` removed before modeling to prevent data leakage
- **Class Balance:** 511 pass · 489 fail — nearly perfectly balanced, so accuracy is a reliable metric and no resampling was needed

| Variable | Type | Description |
|---|---|---|
| `study_hours_per_day` | Numeric | Average daily study hours (0–8.3) |
| `mental_health_rating` | Numeric | Self-reported mental health (1–10) |
| `attendance_percentage` | Numeric | % of classes attended |
| `sleep_hours` | Numeric | Average nightly sleep hours |
| `social_media_hours` | Numeric | Daily hours on social media |
| `netflix_hours` | Numeric | Daily hours on streaming platforms |
| `exercise_frequency` | Numeric | Exercise sessions per week |
| `age` | Numeric | Student age (17–24) |
| `part_time_job` | Factor | Has a part-time job? (Yes/No) |
| `diet_quality` | Factor | Diet quality (Poor/Fair/Good) |
| `internet_quality` | Factor | Internet quality (Poor/Average/Good) |
| `parental_education_level` | Factor | Highest parental education level |
| `extracurricular_participation` | Factor | Participates in extracurriculars? (Yes/No) |
| `gender` | Factor | Gender (Male/Female/Other) |
| `exam_score` | Numeric | Final exam score — used to create pass_fail, then removed |

---

## 🛠️ Methodology

### Pipeline

```
Raw Data → Preprocessing → EDA → Remove exam_score → Train/Test Split
    → 8 Models (all predictors) → Evaluation → Results Comparison
```

### Preprocessing
- Factor encoding for all categorical variables
- Removed `student_id` (no predictive value)
- Checked for missing values with `vis_dat()` and `anyNA()`
- Created `pass_fail` outcome, then **removed `exam_score`** to prevent data leakage

### Models

| Model | Key Setting |
|---|---|
| Logistic Regression (Full) | All predictors, threshold = 0.5 |
| Logistic Regression (Stepwise) | AIC selection, `direction = "both"` |
| Decision Tree (Unpruned) | Full depth |
| Decision Tree (Pruned) | `cp = 0.05` |
| Random Forest | 500 trees, `mtry = floor(sqrt(p))` |
| SVM Linear | Linear kernel |
| SVM Polynomial | Degree 3 |
| SVM Radial | RBF kernel |

### Evaluation
- ✅ Confusion matrix heatmaps
- ✅ Actual vs predicted classification plots
- ✅ Predicted probability distribution (logistic regression)
- ✅ Precision-Recall curves (logistic regression)
- ✅ 10-fold cross-validation on every model
- ✅ Summary metrics table (Accuracy, Sensitivity, Specificity, Kappa, Balanced Accuracy, CV Accuracy)

---

## 📁 Project Structure

```
├── Student Habits & Academic Success — Predictive Modeling.Rmd
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

| # | Question | Key Finding |
|---|---|---|
| Q1 | How do study habits influence the likelihood of passing or failing? | Pass students cluster at **3–6 hrs/day**; fail students mostly under 3 hrs — study time is the clearest separator |
| Q2 | Does mental health affect academic success? | Passing median = **7/10**, failing median = **4/10** — a 3-point gap with barely overlapping distributions |
| Q3 | How do part-time jobs impact academic performance? | Effect is **smaller than expected** — medians only ~1.4 pts apart, challenging the assumption that jobs hurt grades |
| Q4 | How does attendance percentage relate to exam performance? | **Weaker signal** than study time — students with high attendance still failed if study habits were poor |

---

## 🔬 Diagnostic Tests

Run on both logistic regression models to check core assumptions.

| Test | Result | What It Means |
|---|---|---|
| VIF — Full GLM | All values acceptable | No serious multicollinearity in the full model |
| VIF — Stepwise GLM | All values acceptable | Trimming variables kept collinearity low |
| Class Balance Check | 511 pass · 489 fail | Nearly perfect balance — accuracy is a reliable metric, no resampling needed |
| Probability Distribution | Two well-separated peaks | Model assigns high confidence to most predictions — good calibration |
| Precision-Recall Curve | Strong AUC | Model maintains high precision even as recall increases |

---

## 🏆 Model Results

All 8 models were evaluated on a held-out 30% test set and with **10-fold cross-validation**. CV Accuracy reflects the average across 10 folds on the training data.

| Model | Accuracy | Sensitivity | Specificity | Kappa | CV Accuracy |
|---|---|---|---|---|---|
| GLM Full | 92.98% | 92.47% | 93.46% | 0.8594 | 87.45% |
| **GLM Stepwise** ⭐ | **93.31%** | **93.15%** | **93.46%** | **0.8661** | **89.02%** |
| DT Unpruned | 84.62% | 79.45% | 89.54% | 0.6915 | 80.17% |
| DT Pruned | 83.61% | 86.30% | 81.05% | 0.6725 | 79.44% |
| Random Forest | 90.30% | 89.73% | 90.85% | 0.8059 | 85.74% |
| **SVM Linear** ⭐ | **93.31%** | **93.15%** | **93.46%** | **0.8661** | 87.88% |
| SVM Polynomial | 91.30% | 89.73% | 92.81% | 0.8259 | 79.17% |
| SVM Radial | 92.98% | 91.78% | 94.12% | 0.8594 | 86.58% |

> ⭐ **GLM Stepwise** achieved the highest CV accuracy (89.02%) making it the most reliable model overall. **SVM Linear** matched it on test set accuracy and Kappa but had slightly lower CV accuracy.

**Metrics explained:**
- **Sensitivity** — of all students who actually failed, how many did the model correctly identify?
- **Specificity** — of all students who actually passed, how many did the model correctly identify?
- **Kappa** — accuracy adjusted for chance agreement (> 0.8 = strong)
- **CV Accuracy** — most reliable metric; averaged across 10 train/validation splits

---

## 🔍 Key Findings

- 📚 **Study hours per day** was the single strongest predictor across all models. The random forest variable importance plot confirms this clearly.
- 🧠 **Mental health** had a meaningful effect — students with lower self-reported mental health scores were significantly more likely to fail.
- 💼 **Part-time jobs** had a surprisingly small impact. The data does not support the common assumption that working strongly hurts grades.
- 🏫 **Attendance alone** was a weak predictor. Quality of study time matters more than simply showing up.
- 🔬 **Stepwise logistic regression** trimmed the predictor set to only the most informative variables — comparing it to the full model reveals which lifestyle factors are genuinely independent contributors.
- 🏆 **GLM Stepwise** was the best overall model with the highest CV accuracy (89.02%), strong test accuracy (93.31%), and a Kappa of 0.866.

---

## 📌 Project Summary

This project applies eight classification models to predict whether a student passes or fails based on lifestyle and habit data from 1,000 students. The dataset was nearly perfectly balanced (511 pass / 489 fail), making accuracy a reliable metric without any resampling. Stepwise logistic regression came out on top with 93.31% test accuracy and 89.02% CV accuracy — the best of any model.

The clearest finding: **study hours per day and mental health are the two variables that actually separate passing from failing students.** Part-time jobs and attendance, both commonly assumed to matter a lot, turned out to be much weaker signals than expected.

---

## ⚠️ Limitations

- **Fixed pass/fail threshold.** Using 70 as the cutoff is a reasonable starting point but means a student scoring 69 and one scoring 40 are treated the same — some nuance in the outcome is lost.
- **Self-reported variables.** Study hours, sleep, and mental health ratings are self-reported, so actual behavior may not perfectly match what students logged.
- **Small dataset.** 1,000 rows is workable but on the smaller side for comparing eight models — results could shift with a larger sample.
- **No institutional context.** There's no information about school type, course difficulty, or country, which likely affect both habits and outcomes.

---

## ▶️ How to Run

> 🌐 **View the full published report on RPubs:** [Student Habits & Academic Success](https://rpubs.com/Priesthood162002/1439164)

1. Clone or download this repository
2. Place `student_habits_performance.csv` in the same folder as the `.Rmd` file
3. Open `Student Habits & Academic Success — Predictive Modeling.Rmd` in RStudio
4. Install required packages and knit locally:

```r
install.packages(c(
  "dplyr", "ggplot2", "e1071", "corrplot", "caret", "kernlab",
  "visdat", "car", "PRROC", "rpart", "rpart.plot",
  "pROC", "randomForest", "reshape2", "scales"
))
```

> 💡 `kernlab` is required for `svmLinear`, `svmPoly`, and `svmRadial` inside caret's `train()`.

---

## 🧰 Skills Demonstrated

`R` · `RMarkdown` · `ggplot2` · `caret` · `Binary Classification` · `Logistic Regression` · `Stepwise Selection` · `Decision Trees` · `Random Forest` · `SVM` · `10-Fold Cross-Validation` · `EDA` · `Data Leakage Prevention` · `Custom Plot Functions` · `Reproducible Research`

---

## 🙋 Author
Made by **Royalpriesthood Olola** · [GitHub](https://github.com/Royalpriesthood3260) · [LinkedIn](https://www.linkedin.com/in/royalpriesthoodolola)

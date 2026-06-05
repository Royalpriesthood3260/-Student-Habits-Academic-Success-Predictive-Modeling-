# 🎓 Student Habits & Academic Success — Predictive Modeling in R

![Language](https://img.shields.io/badge/Language-R-276DC3?style=flat-square&logo=r)
![Models](https://img.shields.io/badge/Models-8%20Classifiers-brightgreen?style=flat-square)
![CV](https://img.shields.io/badge/Validation-10--Fold%20CV-orange?style=flat-square)
![Dataset](https://img.shields.io/badge/Dataset-1%2C000%20Students-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-success?style=flat-square)

**Author:** Royalpriesthood Olola | UEC671 &nbsp;·&nbsp; **Date:** May 2025

---

## 📌 Overview

Can lifestyle habits predict whether a student passes or fails? This project answers that question by combining exploratory data analysis with eight machine learning classification models applied to a dataset of 1,000 students.

Variables include study time, sleep, mental health, social media use, diet quality, internet quality, part-time job status, parental education, and more. The outcome variable is a binary **pass/fail** label derived from final exam scores (threshold = 70).

The goal is not just accuracy — it's interpretability. Which habits matter most? Which assumptions about student life hold up in the data?

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

## 🏆 Model Results

All 8 models were evaluated on a held-out 30% test set and with **10-fold cross-validation**. Results below are from the test set; CV Accuracy reflects the average across 10 folds on the training data.

| Model | Accuracy | Sensitivity | Specificity | Kappa | CV Accuracy |
|---|---|---|---|---|---|
| GLM Full | — | — | — | — | — |
| **GLM Stepwise** | — | — | — | — | — |
| DT Unpruned | — | — | — | — | — |
| DT Pruned | — | — | — | — | — |
| **Random Forest** ⭐ | — | — | — | — | — |
| SVM Linear | — | — | — | — | — |
| SVM Polynomial | — | — | — | — | — |
| SVM Radial | — | — | — | — | — |

> ⚠️ **Note:** Fill in the actual metric values after knitting `Final_Project_Improved.Rmd`. The ⭐ marks the expected best performer based on CV accuracy — update if your results differ.

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
- 🌲 **Random Forest** and **SVM variants** consistently achieved the highest and most stable accuracy across cross-validation folds.

---

## 🗂️ Dataset

- **Source:** [Kaggle — Student Habits vs Academic Performance](https://www.kaggle.com/datasets/jayaantanaath/student-habits-vs-academicperformance)
- **Size:** 1,000 students · 16 variables · No missing values
- **Outcome:** `pass_fail` — binary label created from `exam_score` (≥ 70 = pass), then `exam_score` removed before modeling to prevent data leakage

<details>
<summary><b>Click to expand variable descriptions</b></summary>

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

</details>

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
├── Final_Project_Improved.Rmd     # Full analysis — knit to HTML in RStudio
├── Project_Walkthrough.md         # Plain English explanation of every code decision
├── Proposal_Revised.md            # Formal project proposal
├── student_habits_performance.csv # Dataset (or download from Kaggle)
└── README.md                      # This file
```

---

## ▶️ How to Run

1. Clone or download this repository
2. Place `student_habits_performance.csv` in the same folder as the `.Rmd` file
3. Open `Final_Project_Improved.Rmd` in RStudio
4. Install required packages:

```r
install.packages(c(
  "dplyr", "ggplot2", "e1071", "corrplot", "caret", "kernlab",
  "visdat", "car", "PRROC", "rpart", "rpart.plot",
  "pROC", "randomForest", "reshape2", "scales"
))
```

5. Click **Knit** → generates a self-contained HTML report

> 💡 `kernlab` is required for `svmLinear`, `svmPoly`, and `svmRadial` inside caret's `train()`.

---

## 💡 What I Learned

- **Data leakage is subtle.** Keeping `exam_score` in the model — even accidentally — would have produced artificially perfect accuracy. Identifying and fixing this was one of the most important steps in the project.
- **Threshold choice matters.** Using `> 0.70` instead of `> 0.5` as the logistic regression decision boundary changes sensitivity and specificity in ways that make model comparisons unfair. The standard 0.5 cutoff is the correct default.
- **More predictors is not always better, but here it helped.** Including all lifestyle and demographic variables rather than just a numeric subset gave the models richer information to work with, and the stepwise model identified which ones genuinely added value.
- **Cross-validation over a single split.** A single 70/30 split can be lucky or unlucky. 10-fold CV averages across 10 different splits and gives a much more trustworthy picture of how each model would generalize.
- **Visual evaluation tells stories numbers can't.** A confusion matrix heatmap, an actual vs predicted jitter plot, and a probability distribution plot each reveal different aspects of model behavior that raw accuracy numbers hide.

---

## 🧰 Skills Demonstrated

`R` · `RMarkdown` · `ggplot2` · `caret` · `Binary Classification` · `Logistic Regression` · `Stepwise Selection` · `Decision Trees` · `Random Forest` · `SVM` · `10-Fold Cross-Validation` · `EDA` · `Data Leakage Prevention` · `Custom Plot Functions` · `Reproducible Research`

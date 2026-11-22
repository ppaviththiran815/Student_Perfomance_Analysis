# Student Performance Analysis

> **Syntecxhub Data Analysis Internship, Project 2**

An end-to-end analysis of the factors that influence student exam performance. The project cleans the data, explores it with statistics and visualizations, and builds regression models to predict a student's final exam score.

---

## Table of Contents

1. [Objective](#objective)
2. [Dataset](#dataset)
3. [Tools and Libraries](#tools-and-libraries)
4. [Project Workflow](#project-workflow)
5. [Key Results](#key-results)
6. [Insights and Recommendations](#insights-and-recommendations)
7. [Repository Structure](#repository-structure)
8. [How to Run](#how-to-run)
9. [Limitations and Future Work](#limitations-and-future-work)
10. [Author](#author)

---

## Objective

- Load and preprocess a student dataset (marks, attendance, study hours, and more)
- Analyze overall performance trends
- Identify the factors that affect exam performance (study hours, attendance, sleep, parental involvement, motivation, etc.)
- Compare performance across different groups (gender, school type, family income, and others)
- Visualize the findings with charts
- Build predictive models and generate insights for improving academic results

---

## Dataset

- **Name:** Student Performance Factors (Kaggle)
- **File:** `StudentPerformance.csv`
- **Size:** 6,607 rows and 20 columns
- **Target variable:** `Exam_Score`

| Type | Columns |
|---|---|
| Numerical | `Hours_Studied`, `Attendance`, `Sleep_Hours`, `Previous_Scores`, `Tutoring_Sessions`, `Physical_Activity`, `Exam_Score` |
| Categorical | `Parental_Involvement`, `Access_to_Resources`, `Extracurricular_Activities`, `Motivation_Level`, `Internet_Access`, `Family_Income`, `Teacher_Quality`, `School_Type`, `Peer_Influence`, `Learning_Disabilities`, `Parental_Education_Level`, `Distance_from_Home`, `Gender` |

> **Source:** [Kaggle: Student Performance Factors](https://www.kaggle.com/) *(add the exact dataset link here)*

---

## Tools and Libraries

- **Language:** Python 3
- **Environment:** Jupyter Notebook / Google Colab
- **Data handling:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`
- **Machine learning:** `scikit-learn` (Linear Regression, Ridge, SVR, MinMaxScaler, train_test_split)

---

## Project Workflow

### 1. Data Loading and Inspection
- Loaded the CSV with pandas and checked its shape, data types, and summary statistics (`head`, `info`, `describe`).
- Reviewed numerical and categorical columns separately.

### 2. Data Cleaning
- Checked for missing values across all columns.
- Filled missing values in three categorical columns with the **mode** (most frequent value):
  - `Teacher_Quality`
  - `Parental_Education_Level`
  - `Distance_from_Home`

### 3. Descriptive Analysis
- Calculated the range, mean, and standard deviation of `Exam_Score`.
- Counted students scoring above the class average.
- Calculated the mean and standard deviation of `Hours_Studied`.

### 4. Exploratory Data Analysis (EDA)
- **Distribution:** histogram with KDE of exam scores
- **Relationships:** scatter plots of Hours Studied vs. Exam Score (by gender), Sleep Hours vs. Exam Score (by parental involvement), and Previous Scores vs. Exam Score (by motivation level)
- **Group comparison:** box plots of every categorical feature against exam score, with focused plots for Parental Involvement and Motivation Level
- **Correlation:** heatmap of all numerical features
- **Feature relationships:** count plots such as Motivation vs. Parental Involvement, Family Income vs. Learning Disabilities, Teacher Quality vs. School Type, Peer Influence vs. Motivation, and Family Income vs. School Type

### 5. Feature Engineering
- Converted categorical columns to numeric using one-hot encoding (`pd.get_dummies`, `drop_first=True`), giving **27 input features**.
- Split the data **85% train / 15% test** (`random_state=42`).
- Created a MinMax-scaled version of the features.

### 6. Modeling
Three regression models were trained to predict `Exam_Score`:
- Linear Regression
- Ridge Regression (alpha = 1.0)
- Support Vector Regression (SVR)

Each model was evaluated with Mean Squared Error (MSE) and R² score, and visualized with True vs. Predicted plots.

---

## Key Results

### Exam score summary

| Metric | Value |
|---|---|
| Mean exam score | 67.24 |
| Standard deviation | 3.89 |
| Score range (max - min) | 46 |
| Students above average | 3,008 of 6,607 |
| Mean hours studied | 19.98 hours (std 5.99) |

### Model comparison

| Model | MSE | Train R² | Test R² |
|---|---|---|---|
| Linear Regression | 2.915 | 0.716 | **0.797** |
| Ridge Regression | 2.915 | 0.716 | **0.797** |
| SVR | 4.645 | 0.592 | 0.677 |

**Best models:** Linear and Ridge Regression perform almost identically, explaining about **80% of the variance** in exam scores on unseen data. SVR performs noticeably worse.

---

## Insights and Recommendations

> *Fill in the specific numbers from your own heatmap and box plots before publishing.*

1. **Study habits matter.** Hours studied and attendance are among the strongest numerical drivers of exam score. *(Add the correlation values from your heatmap.)*
2. **Past performance predicts future performance.** `Previous_Scores` shows a clear positive relationship with `Exam_Score`, so early intervention for low scorers is important.
3. **Support systems make a difference.** Students with higher parental involvement and motivation tend to score higher in the box plots.
4. **Scores are fairly tightly clustered** (std of about 3.9 around a mean of about 67), so even small improvements in study habits and attendance can move a student noticeably.
5. **Simple models work well.** Linear and Ridge Regression reach about 0.80 R², which suggests the relationships in this dataset are largely linear.

**Recommendations for improving academic results:**
- Encourage consistent attendance and structured study hours.
- Offer tutoring and extra support to students with low previous scores.
- Involve parents and build motivation programs for low-engagement students.
- Ensure access to resources and quality teaching across all school types and income groups.

---

## Repository Structure

```
Syntecxhub_Student_Performance_Analysis/
│
├── StudentsPerfomance_Analysis.ipynb   # Main analysis notebook
├── StudentPerformance.csv              # Dataset
├── README.md                           # Project documentation
└── images/                             # (optional) screenshots of key charts
```

---

## How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/Syntecxhub_Student_Performance_Analysis.git
   cd Syntecxhub_Student_Performance_Analysis
   ```

2. **Install dependencies**
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```

3. **Launch the notebook**
   ```bash
   jupyter notebook StudentsPerfomance_Analysis.ipynb
   ```

4. Make sure `StudentPerformance.csv` is in the same folder as the notebook, then run all cells.

---

## Limitations and Future Work

- The dataset contains a single overall exam score, so subject-wise analysis is not possible.
- The analysis shows **correlation, not causation**.
- Future improvements:
  - Try tree-based models (Random Forest, Gradient Boosting) and compare feature importance
  - Tune hyperparameters with `GridSearchCV`
  - Add an interactive dashboard (Power BI, Tableau, or Streamlit)
  - Add statistical tests (t-test, ANOVA) for group comparisons

---

## Author

**Shivam Sachan**
Data Analysis Intern, [Syntecxhub](https://www.syntecxhub.com)

- LinkedIn: *(add your profile link)*
- GitHub: *(add your profile link)*

---

*Completed as part of the Syntecxhub Internship Program. #Syntecxhub*

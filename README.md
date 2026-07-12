# 🏦 Loan Approval Prediction

Predicting whether a bank loan application will be **Approved** or **Rejected** using Exploratory Data Analysis and Machine Learning.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)
![Scikit--learn](https://img.shields.io/badge/Scikit--learn-Machine%20Learning-F7931E?logo=scikit-learn&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4c72b0)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Screenshots](#-screenshots)
- [About the Dataset](#-about-the-dataset)
- [Project Workflow](#-project-workflow)
- [Exploratory Data Analysis — Key Insights](#-exploratory-data-analysis--key-insights)
- [Feature Engineering](#-feature-engineering)
- [Correlation Analysis](#-correlation-analysis)
- [Machine Learning Models](#-machine-learning-models)
- [Model Evaluation & Results](#-model-evaluation--results)
- [Conclusion](#-conclusion)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Future Improvements](#-future-improvements)
- [Author](#-author)
- [License](#-license)

---

## 📖 Overview

The goal of this project is to **predict whether a loan application will be approved by a bank**, based on an applicant's financial and personal profile — including CIBIL score, annual income, loan amount, loan tenure, number of dependents, education, employment status, and asset holdings.

Through in-depth **Exploratory Data Analysis (EDA)**, this project uncovers the key factors that influence loan approval decisions. These insights can help financial institutions:

- Identify high-priority applicants likely to be approved
- Design targeted offers for high-CIBIL-score customers
- Understand risk factors tied to rejection

Two classification models — **Decision Tree** and **Random Forest** — are trained and compared to predict the final loan status.

---

## 🖼 Screenshots

> Place your screenshot images inside a `screenshots/` folder in the repository root, then they will render automatically below.

# | Model Results |
|:---:|:---:|:---:|
<img width="1517" height="725" alt="Screenshot 2026-07-12 121410" src="https://github.com/user-attachments/assets/92560c06-f9eb-4c67-a659-387e552805d5" />

<img width="1512" height="736" alt="Screenshot 2026-07-12 121448" src="https://github.com/user-attachments/assets/30e51fbd-b152-4d9d-8c0f-ea6335f8181b" />






## 📊 About the Dataset

The **Loan Approval Dataset** contains financial and demographic records used to determine loan eligibility. Key columns include:

| Feature | Description |
|---|---|
| `no_of_dependents` | Number of dependents of the applicant |
| `education` | Graduate / Not Graduate |
| `self_employed` | Employment type (Yes/No) |
| `income_annum` | Annual income of the applicant |
| `loan_amount` | Requested loan amount |
| `loan_term` | Loan repayment tenure |
| `cibil_score` | Applicant's credit score |
| `residential_assets_value` | Value of residential assets |
| `commercial_assets_value` | Value of commercial assets |
| `luxury_assets_value` | Value of luxury assets |
| `bank_asset_value` | Value of bank assets |
| `loan_status` | Target variable — Approved / Rejected |

---

## 🔄 Project Workflow

```
Data Loading → Data Cleaning → Feature Engineering → EDA →
Label Encoding → Correlation Analysis → Train/Test Split →
Model Training (Decision Tree, Random Forest) → Evaluation → Conclusion
```

### Data Preprocessing
- Removed the `loan_id` identifier column (irrelevant to prediction).
- Checked for null values and validated data types.
- Combined the four asset columns into two engineered features for simpler interpretation:
  - **Movable Assets** = Bank Assets + Luxury Assets
  - **Immovable Assets** = Residential Assets + Commercial Assets

---

## 🔍 Exploratory Data Analysis — Key Insights

Univariate, bivariate, and target-relationship analyses were performed using `seaborn`/`matplotlib` to uncover approval trends:

- **Number of Dependents:** No strong effect on approval, although rejections rise slightly with more dependents.
- **Education vs. Income:** Graduates and non-graduates have nearly the same median income — education alone is **not** a major driver of approval.
- **Self-Employment:** Most graduates are salaried, while most non-graduates are self-employed — an indirect proxy for income stability.
- **Loan Amount vs. Tenure:** Larger loans tend to have shorter approved tenures.
- **CIBIL Score Distribution:** Most applicants fall in the "Poor–Fair" range (below 649), but scores above ~600 correlate strongly with approval.
- **Assets vs. Loan Status:** Higher movable and immovable assets significantly increase approval likelihood — assets act as loan security.
- **Annual Income vs. Loan Status:** Approved applicants trend slightly higher in income, though the difference is modest.

### 🏆 Strongest Predictor: CIBIL Score

| CIBIL Score Range | Rating |
|---|---|
| 300–549 | Poor |
| 550–649 | Fair |
| 650–749 | Good |
| 750–799 | Very Good |
| 800–900 | Excellent |

Applicants with a **CIBIL score above ~600** show a dramatically higher approval rate — this turned out to be the **single strongest predictor** in the dataset.

---

## 🛠 Feature Engineering

- Combined 4 raw asset columns → **2 engineered features** (`Movable_assets`, `Immovable_assets`)
- **Label Encoding** applied to categorical variables:
  - `education`: Not Graduate = 0, Graduate = 1
  - `self_employed`: No = 0, Yes = 1
  - `loan_status`: Rejected = 0, Approved = 1

---

## 🔗 Correlation Analysis

A correlation heatmap revealed the strongest relationships in the dataset:

- Movable Assets ↔ Immovable Assets
- Income ↔ Movable / Immovable Assets
- Loan Amount ↔ Movable / Immovable Assets
- Loan Amount ↔ Annual Income
- **Loan Status ↔ CIBIL Score** (most important for prediction)

---

## 🤖 Machine Learning Models

The dataset was split **80/20** into training and testing sets. Two classification algorithms were trained and compared:

| Model | Library |
|---|---|
| Decision Tree Classifier | `sklearn.tree.DecisionTreeClassifier` |
| Random Forest Classifier | `sklearn.ensemble.RandomForestClassifier` |

---

## 📈 Model Evaluation & Results

Models were evaluated using **Confusion Matrix**, **Classification Report**, **R² Score**, **MSE**, and **MAE**, along with actual-vs-predicted distribution plots.

| Model | Approx. Accuracy | Notes |
|---|:---:|---|
| **Decision Tree Classifier** | **~91.4%** | ✅ Fewer misclassifications, best overall fit |
| Random Forest Classifier | ~89.4% | Slightly more false positives/negatives |

> 🏅 **The Decision Tree Classifier outperformed the Random Forest Classifier** on this dataset, showing tighter overlap between actual and predicted values and a lower error rate.

---

## ✅ Conclusion

Based on the EDA and modeling results, the following factors were found to be most influential in loan approval decisions:

- 📊 **CIBIL Score** — Higher scores → significantly higher approval chances
- 👨‍👩‍👧 **Number of Dependents** — More dependents → slightly lower approval chances
- 🏠 **Assets (Movable & Immovable)** — More assets → higher approval chances
- 💰 **Loan Amount & Tenure** — Higher amount with shorter tenure → higher approval chances

Between the two models tested, the **Decision Tree Classifier (91.4% accuracy)** proved to be the better-performing model compared to the **Random Forest Classifier (89.4% accuracy)** for this dataset.

---

## 🧰 Tech Stack

- **Language:** Python 3
- **Data Manipulation:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
- **Machine Learning:** Scikit-learn
- **Environment:** Jupyter Notebook

---

## 📁 Project Structure

```
Loan-Approval-Prediction/
│
├── Loan_Approval_Prediction.ipynb   # Main analysis & modeling notebook
├── loan_approval_dataset.csv        # Dataset (add your own copy here)
├── screenshots/                     # Project screenshots for this README
│   ├── screenshot-1.png
│   ├── screenshot-2.png
│   └── screenshot-3.png
├── README.md                        # Project documentation
└── LICENSE
```

---

## 🚀 Getting Started

### Prerequisites
Make sure you have Python 3 and the following libraries installed:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

### Run Locally

```bash
# Clone the repository
git clone https://github.com/<your-username>/Loan-Approval-Prediction.git
cd Loan-Approval-Prediction

# Launch Jupyter Notebook
jupyter notebook Loan_Approval_Prediction.ipynb
```

Make sure `loan_approval_dataset.csv` is placed in the same directory as the notebook before running the cells.

---

## 🔮 Future Improvements

- Hyperparameter tuning (GridSearchCV) for both models
- Try additional algorithms (XGBoost, Logistic Regression, SVM)
- Handle class imbalance if present
- Deploy the best model as a web app (Streamlit/Flask) for live predictions
- Add cross-validation for more robust accuracy estimates

---

## 👤 Author

**Shubham**

If you found this project helpful, consider giving it a ⭐ on GitHub!

---

## 📄 License

This project is licensed under the **MIT License** — feel free to use, modify, and distribute with attribution.

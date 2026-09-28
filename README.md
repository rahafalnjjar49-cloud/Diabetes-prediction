# 🩺 Diabetes Prediction


A machine learning project that predicts whether a patient has diabetes based on medical measurements. It compares five classification algorithms and includes a **Streamlit web app** for interactive predictions.

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Project Workflow](#-project-workflow)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Models & Results](#-models--results)
- [Streamlit App](#-streamlit-app)
- [Requirements](#-requirements)
- [How to Run](#-how-to-run)
- [Project Structure](#-project-structure)
- [Limitations & Future Work](#-limitations--future-work)
- [Disclaimer](#-disclaimer)

---

## 🔎 Overview

The goal is to build a binary classifier that predicts diabetes (`Outcome`: 1 = diabetic, 0 = non-diabetic) from 8 clinical features. The project covers:

- Data loading, inspection, and cleaning checks.
- Exploratory data analysis (class balance, correlations, distributions).
- Training and comparing five classifiers.
- Saving the trained models with `joblib`.
- Deploying an interactive prediction app with Streamlit.

## 📊 Dataset

| Item | Details |
|---|---|
| **Name** | Pima Indians Diabetes Dataset |
| **Samples** | 768 |
| **Features** | 8 numeric features |
| **Target** | `Outcome` (0 = No diabetes, 1 = Diabetes) |
| **Missing values** | None (no nulls) |
| **Duplicates** | None |

**Features:** `Pregnancies`, `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, `BMI`, `DiabetesPedigreeFunction`, `Age`

**Class distribution:**

- 🟢 Non-diabetic (0): **500** samples
- 🔴 Diabetic (1): **268** samples

> Place `diabetes.csv` in the same directory as the notebook. The dataset is available on [Kaggle](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database).

## 🛠️ Project Workflow

1. **Import libraries** (pandas, numpy, matplotlib, seaborn, scikit-learn).
2. **Load the data** from `diabetes.csv`.
3. **Inspect the data:** `info()`, `describe()`, duplicate and null checks.
4. **Explore:** class distribution, feature correlations, and distribution plots.
5. **Split:** 80% training (614 samples) / 20% testing (154 samples), `random_state=42`.
6. **Train** five models and evaluate each on the test set.
7. **Save** all models as `.pkl` files.
8. **Deploy** a Streamlit app that loads the saved models.

## 📈 Exploratory Data Analysis

Correlation of each feature with the target (`Outcome`):

| Feature | Correlation |
|---|---|
| Glucose | 0.467 |
| BMI | 0.293 |
| Age | 0.238 |
| Pregnancies | 0.222 |
| DiabetesPedigreeFunction | 0.174 |
| Insulin | 0.131 |
| SkinThickness | 0.075 |
| BloodPressure | 0.065 |

**Glucose** is the strongest predictor, followed by **BMI** and **Age**.

## 🏆 Models & Results

All models were evaluated on the same test set (154 samples) using default hyperparameters.

| Model | Accuracy |
|---|---|
| Naive Bayes (GaussianNB) | **76.62%** |
| Support Vector Machine (SVC) | **76.62%** |
| Decision Tree | 75.97% |
| Gradient Boosting | 74.03% |
| Random Forest | 73.38% |

### Detailed Metrics (Diabetic class = 1)

| Model | Precision | Recall | F1-score |
|---|---|---|---|
| Naive Bayes | 0.66 | 0.71 | 0.68 |
| Decision Tree | 0.64 | 0.75 | 0.69 |
| SVM | 0.72 | 0.56 | 0.63 |
| Random Forest | 0.62 | 0.64 | 0.63 |
| Gradient Boosting | 0.63 | 0.67 | 0.65 |

**Key takeaways:**

- Naive Bayes and SVM tie for the highest accuracy.
- The Decision Tree has the highest recall for diabetic patients (0.75), which matters in screening since missing a positive case is costly.
- SVM has the highest precision for the diabetic class (0.72) but the lowest recall (0.56).

## 🌐 Streamlit App

The notebook generates `app.py`, a web app that lets you:

- Enter patient data in the sidebar (all 8 features).
- Choose which trained model to use.
- Click **Predict** to get a result: *"Diabetes detected"* or *"No Diabetes"*.

The app loads these saved models: `nb.pkl`, `dt.pkl`, `svm.pkl`, `rf.pkl`, `gb.pkl`.

## 📦 Requirements

- Python 3.x
- numpy
- pandas
- matplotlib
- seaborn
- scikit-learn
- joblib
- streamlit

```bash
pip install numpy pandas matplotlib seaborn scikit-learn joblib streamlit
```

## 🚀 How to Run

### Option 1: Google Colab

1. Click the **Open In Colab** badge at the top.
2. Run the cells in order and upload `diabetes.csv` when prompted.
3. The notebook trains the models, saves them, and creates `app.py`.

### Option 2: Run locally

```bash
# 1) Clone the repository
git clone https://github.com/rahafalnjjar49-cloud/Diabetes-prediction.git
cd Diabetes-prediction

# 2) Install dependencies
pip install numpy pandas matplotlib seaborn scikit-learn joblib streamlit jupyter

# 3) Place diabetes.csv in the folder and run the notebook
jupyter notebook Diabetes_prediction.ipynb

# 4) Launch the web app (after the .pkl files and app.py are generated)
streamlit run app.py
```

> ⚠️ The notebook uses `google.colab.files.upload()`, which only works in Colab. When running locally, remove that cell and load the file directly with `pd.read_csv('diabetes.csv')`.

## 📁 Project Structure

```
Diabetes-prediction/
├── Diabetes_prediction.ipynb   # Main notebook
├── diabetes.csv                # Dataset
├── app.py                      # Streamlit app (generated by the notebook)
├── nb.pkl                      # Naive Bayes model
├── dt.pkl                      # Decision Tree model
├── svm.pkl                     # SVM model
├── rf.pkl                      # Random Forest model
├── gb.pkl                      # Gradient Boosting model
└── README.md
```

## 🔧 Limitations & Future Work

- **Invalid zero values:** columns like `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, and `BMI` contain zeros that are physiologically impossible and likely represent missing data. Imputing them (e.g., with the median) may improve results.
- **No feature scaling:** applying `StandardScaler`, especially for SVM, could boost performance.
- **Default hyperparameters:** tuning with `GridSearchCV` or `RandomizedSearchCV` could improve all models.
- **Single split:** using cross-validation would give more reliable performance estimates.
- **Class imbalance:** the data is ~65/35; techniques like SMOTE or class weights could help recall on the diabetic class.
- **Additional models:** try XGBoost / LightGBM for comparison.

## ⚠️ Disclaimer

This project is for **educational purposes only** and must not be used for real medical diagnosis. It is not a substitute for professional medical advice.

---

⭐ If you found this project useful, consider giving the repository a star!

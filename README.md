# ❤️ Heart Disease Prediction — Machine Learning

A machine learning project for predicting heart disease based on patient clinical data. This project applies various classification algorithms to determine the presence or absence of heart disease using medical indicators.

---

## 📋 Table of Contents

- [About the Project](#-about-the-project)
- [Dataset](#-dataset)
- [Installation](#️-installation)
- [Project Structure](#-project-structure)
- [Methodology](#-methodology)
- [Models & Results](#-models--results)
- [Tech Stack](#️-tech-stack)
- [Usage](#-usage)
- [Author](#-author)

---

## 🎯 About the Project

Heart disease is the leading cause of death worldwide. This project aims to build a **binary classification** model that predicts the likelihood of heart disease based on a patient's clinical attributes such as age, blood pressure, cholesterol level, and more.

**Goal:** Classify whether a patient **has heart disease (1)** or **is healthy (0)**.

---

## 📊 Dataset

- **Source:** UCI Heart Disease Dataset (Cleveland, Hungarian, Switzerland, VA Long Beach)
- **File:** `data/heart_disease.csv`
- **Size:** 1,024 records, 15 columns (original)
- **Target:** `target_binary` — 0 (healthy) or 1 (disease)

### Feature Descriptions

| Feature | Description | Type |
|---------|-------------|------|
| `age` | Age of the patient (years) | Numerical |
| `sex` | Sex (1 = male, 0 = female) | Categorical |
| `cp` | Chest pain type (1–4) | Categorical |
| `trestbps` | Resting blood pressure (mm Hg) | Numerical |
| `chol` | Serum cholesterol (mg/dl) | Numerical |
| `fbs` | Fasting blood sugar > 120 mg/dl (1 = true, 0 = false) | Categorical |
| `restecg` | Resting ECG results (0–2) | Categorical |
| `thalach` | Maximum heart rate achieved | Numerical |
| `exang` | Exercise-induced angina (1 = yes, 0 = no) | Categorical |
| `oldpeak` | ST depression induced by exercise | Categorical |
| `slope` | Slope of the peak exercise ST segment | Categorical |
| `ca` | Number of major vessels colored by fluoroscopy (0–3) | Categorical |
| `thal` | Thalassemia (3 = normal, 6 = fixed defect, 7 = reversible defect) | Categorical |
| `target_binary` | Target variable (0 = healthy, 1 = disease) | Categorical |

### Target Distribution

```
target_binary
0    554  (54.1%)
1    470  (45.9%)
```

> The dataset is relatively balanced — no significant class imbalance.

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/sarmuh/Heart-Disease-Predict-ML.git
cd Heart-Disease-Predict-ML
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

- **Windows:**
```bash
venv\Scripts\activate
```

- **macOS / Linux:**
```bash
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 📁 Project Structure

```
Heart-Disease-Predict-ML/
│
├── data/
│   └── heart_disease.csv          # Raw dataset
│
├── notebooks/
│   └── data_info_train.ipynb      # EDA, preprocessing & model training
│
├── models/
│   └── RandomF_model.joblib       # Best saved model (Random Forest)
│
├── requirements.txt               # Python dependencies
├── .gitignore
└── README.md
```

---

## 🔬 Methodology

### 1. Data Preprocessing

- The `num` column (multi-class target) was dropped — only `target_binary` was used for binary classification
- **Numerical features:** `age`, `trestbps`, `chol`, `thalach`
- **Categorical features:** `sex`, `cp`, `fbs`, `restecg`, `exang`, `oldpeak`, `slope`, `ca`, `thal`
- **StandardScaler** was applied to numerical features via `ColumnTransformer`

### 2. Train / Test Split

```
Train: 819 samples (80%)
Test:  205 samples (20%)
Random state: 42
```

### 3. Model Selection & Hyperparameter Tuning

**GridSearchCV** with 5-fold Cross-Validation was used for all models to find the optimal hyperparameters.

---

## 📈 Models & Results

### KNN (K-Nearest Neighbors)

- Optimal `n_neighbors` found via **GridSearchCV**
- **Best parameter:** `n_neighbors = 9`
- **CV Best Score:** 0.8547

| Metric | Class 0 | Class 1 | Weighted Avg |
|--------|---------|---------|--------------|
| Precision | 0.85 | 0.83 | 0.84 |
| Recall | 0.87 | 0.82 | 0.84 |
| F1-score | 0.86 | 0.82 | 0.84 |

**Test Accuracy:** 84%

---

### XGBoost

- Hyperparameters tuned via **GridSearchCV**
- **Best parameters:** `learning_rate=0.07`, `max_depth=4`, `n_estimators=300`
- **CV Best Score (F1):** 0.8825

| Metric | Class 0 | Class 1 | Weighted Avg |
|--------|---------|---------|--------------|
| Precision | 0.86 | 0.81 | 0.83 |
| Recall | 0.84 | 0.83 | 0.83 |
| F1-score | 0.85 | 0.82 | 0.83 |

**Test Accuracy:** 83%

---

### 🏆 Random Forest (Best Model)

- Hyperparameters tuned via **GridSearchCV**
- **Best parameters:** `max_depth=5`, `min_samples_leaf=1`, `min_samples_split=2`, `n_estimators=200`
- **CV Best Score (F1):** 0.8838

| Metric | Class 0 | Class 1 | Weighted Avg |
|--------|---------|---------|--------------|
| Precision | 0.89 | 0.90 | 0.89 |
| Recall | 0.92 | 0.86 | 0.89 |
| F1-score | 0.90 | 0.88 | 0.89 |

**Test Accuracy:** 89% ✅

> Random Forest achieved the highest performance across all metrics and was saved to `models/RandomF_model.joblib`.

---

### Model Comparison

| Model | Test Accuracy | CV Best F1 | Precision | Recall |
|-------|---------------|-----------|-----------|--------|
| KNN (k=9) | 84% | 0.8547 | 0.84 | 0.84 |
| XGBoost | 83% | 0.8825 | 0.83 | 0.83 |
| **Random Forest** | **89%** | **0.8838** | **0.89** | **0.89** |

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| Python | 3.11+ | Core programming language |
| NumPy | 2.3.5 | Numerical computing |
| Pandas | 2.3.3 | Data manipulation & analysis |
| Scikit-learn | 1.8.0 | ML models & preprocessing |
| Matplotlib | 3.10.8 | Data visualization |
| Seaborn | 0.13.2 | Statistical visualization |
| XGBoost | 3.2.0 | Gradient boosting model |
| LightGBM | 4.6.0 | Gradient boosting model |
| CatBoost | 1.2.10 | Gradient boosting model |
| Imbalanced-learn | 0.14.1 | Handling imbalanced datasets |
| Joblib | 1.5.3 | Model serialization |

---

## 🚀 Usage

### Load the saved model and make predictions

```python
import joblib
import numpy as np

# Load the model
model = joblib.load("models/RandomF_model.joblib")

# New patient data (13 features)
# [age, trestbps, chol, thalach, sex, cp, fbs, restecg, exang, oldpeak, slope, ca, thal]
new_patient = np.array([[55, 130, 250, 150, 1, 4, 0, 2, 1, 1.5, 2, 1.0, 3.0]])

# Predict
prediction = model.predict(new_patient)
print(f"Result: {'Heart disease detected ⚠️' if prediction[0] == 1 else 'Healthy ✅'}")
```

### Run the Jupyter Notebook

```bash
jupyter notebook notebooks/data_info_train.ipynb
```

---

## 📝 License

This project is open-source and intended for educational purposes.

---

## 👤 Author

**Sarmuh** — [GitHub Profile](https://github.com/sarmuh)

 <p align="center"> M115 Lab 1 — Phishing URL Detection</p>
 <p align="center"> EDA, Parameterized Logistic Regression & SHAP Explainability </p>

<p align="center">
  <strong>ENSIASD Taroudant — Ibn Zohr University</strong><br>
  Master in Intelligent Systems and Cyber Defense<br>
  Module: M115 — AI & Intelligent Systems<br>
  Academic Year: 2026–2027
</p>

---

## 1. Project Overview

This project focuses on detecting phishing URLs using Machine Learning techniques and explaining model predictions through SHAP (SHapley Additive exPlanations).

The main objective is to build a classification system capable of distinguishing between legitimate and phishing websites based on URL-related and website-related features.

The project follows a complete Machine Learning workflow, including Exploratory Data Analysis (EDA), data preprocessing, Logistic Regression modeling, model evaluation, feature interpretation, and security-oriented threshold analysis.

The results are intended to support cybersecurity awareness and help SOC analysts understand phishing detection decisions.

## 2. Project Objectives

- Explore and understand the phishing URL dataset.
- Perform Exploratory Data Analysis (EDA).
- Identify relevant features for phishing detection.
- Prepare and preprocess the dataset.
- Implement and compare Logistic Regression models.
- Apply L1 and L2 regularization.
- Evaluate model performance using classification metrics.
- Interpret model predictions using SHAP.
- Analyze the impact of different classification thresholds.
- Discuss the results from a cybersecurity perspective.

## 3. Dataset Description

**Dataset:** PhiUSIIL Phishing URL Dataset

**Source:** [Kaggle — PhiUSIIL Phishing URL Dataset](https://www.kaggle.com/datasets/kaggleprollc/phishing-url-websites-dataset-phiusiil)

The dataset contains 235,795 website records and 55 columns in the Kaggle version used for this project.

It includes URL characteristics, domain information, security indicators, and website-related features.

### Target Variable

The original dataset contains a column named `label`:

| Original label | Meaning |
|---|---|
| 1 | Legitimate website |
| 0 | Phishing website |

For this project, the target variable is transformed into:

```python
df["IsPhishing"] = 1 - df["label"]
```

Therefore:

| IsPhishing | Meaning |
|---|---|
| 1 | Phishing |
| 0 | Legitimate |

This transformation makes phishing the positive class.

## 4. Exploratory Data Analysis (EDA)

Exploratory Data Analysis is performed to understand the dataset, examine the target distribution, and identify relationships between features.

### 4.1 Dataset Distribution

The class distribution illustrates the number of legitimate and phishing websites.

<p align="center">
  <img width="585" height="331" alt="Phishing and legitimate class distribution" src="https://github.com/user-attachments/assets/95c2c764-3e74-42f8-a6bb-795ce2ed859d">
</p>

### 4.2 Feature Correlation Analysis

The correlation heatmap helps identify relationships between numerical features and detect potentially relevant indicators for phishing classification.

<p align="center">
  <img width="587" height="437" alt="Feature correlation heatmap" src="https://github.com/user-attachments/assets/426a16aa-b6e6-4ff2-9787-c478d43e92b8">
</p>

## 5. Data Preprocessing

The preprocessing stage includes:

- Creating the binary target variable `IsPhishing`.
- Removing irrelevant identifiers and non-numeric columns.
- Excluding the original target column from the input features.
- Separating input features (X) and target variable (y).
- Splitting the dataset into training and testing sets.
- Using stratified sampling to preserve class proportions.
- Applying StandardScaler to numerical features.

The dataset is divided into:

- 75% Training set
- 25% Testing set

**Important:** The scaler is fitted only on the training data to avoid data leakage.

## 6. Logistic Regression Models

Several Logistic Regression configurations are implemented and compared.

| Model | Configuration |
|---|---|
| M1 | Unregularized Logistic Regression |
| M2 | L2 Regularization — C = 0.001 |
| M3 | Standard L2 Regularization — C = 1.0 |
| M4 | L1 Regularization — C = 0.01 |
| M5 | Class-weighted Logistic Regression |

### Model Performance Comparison

The models are evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- PR-AUC

<p align="center">
 <img width="546" height="182" alt="image" src="https://github.com/user-attachments/assets/c9beaae1-14a7-4791-aa3b-4de88ce18ded" />

</p>

The comparison helps identify the configuration that provides the most suitable balance between phishing detection and false alarms.

## 7. Feature Importance and SHAP Explainability

SHAP is used to interpret the predictions of the selected Logistic Regression model.

It explains how individual features contribute to the model's predictions.

### 7.1 SHAP Feature Importance

The SHAP bar plot displays the most influential features based on their average absolute SHAP values.

<p align="center">
 <img width="500" height="434" alt="image" src="https://github.com/user-attachments/assets/7c468b4e-44a3-424b-abcd-68b9d91918ab" />
</p>

### 7.2 SHAP Summary Plot

The SHAP summary plot illustrates how feature values influence the model output and whether they contribute toward phishing or legitimate predictions.

<p align="center">
  <img width="581" height="437" alt="image" src="https://github.com/user-attachments/assets/29cafa80-479a-4bd4-af49-c1998f9fe2fa" />

</p>

### 7.3 Individual Prediction Explanation

SHAP waterfall plots are also used to explain individual predictions, showing how different features contribute to a specific classification result.

## 8. Security-Oriented Analysis

The project also examines the relationship between classification results and cybersecurity decisions.

### 8.1 Confusion Matrix Analysis

The confusion matrix helps distinguish between:

- **True Positives (TP):** Phishing websites correctly detected.
- **True Negatives (TN):** Legitimate websites correctly classified.
- **False Positives (FP):** Legitimate websites incorrectly classified as phishing.
- **False Negatives (FN):** Phishing websites incorrectly classified as legitimate.

These errors have different security implications, particularly in a SOC environment.

### 8.2 Threshold Analysis

Different classification thresholds are evaluated to understand the trade-off between phishing detection and false alarms.

The selected thresholds are:

<p align="center">
  <img width="548" height="108" alt="image" src="https://github.com/user-attachments/assets/f7c8c033-30aa-45c5-b8ed-2993611262b7" />

</p>

A lower threshold generally increases sensitivity to phishing websites, while a higher threshold can reduce false positives but may miss more phishing attempts.

The appropriate threshold depends on the organization's security policy and operational requirements.

## 9. Technologies and Libraries

The project uses the following tools and libraries:

| Technology | Purpose |
|---|---|
| Python | Programming language |
| Pandas | Data manipulation |
| NumPy | Numerical operations |
| Matplotlib | Data visualization |
| Seaborn | Statistical visualization |
| Scikit-learn | Machine Learning and evaluation |
| SHAP | Model explainability |
| Jupyter Notebook | Development environment |
| Kaggle | Dataset access and notebook execution |
| GitHub | Project version control and sharing |

## 10. Repository Structure

```text
M115-Phishing-URL-Detection/
│
├── M115_Lab1_Phishing_URL_Detection.ipynb
│
├── figures/
│   ├── class_distribution.png
│   ├── correlation_heatmap.png
│   ├── model_comparison.png
│   ├── shap_bar.png
│   ├── shap_summary.png
│   └── threshold_analysis.png
│
└── README.md
```

The dataset is not included in this repository. It can be downloaded from the original Kaggle source linked above.

## 11. How to Run the Project

### Option 1: Google Colab

1. Open the notebook in Google Colab.
2. Add the PhiUSIIL dataset to your Kaggle or Colab environment.
3. Update the dataset path if necessary.
4. Execute the notebook cells in order.

### Option 2: Local Environment

Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/M115-Phishing-URL-Detection.git
```

Navigate to the project directory:

```bash
cd M115-Phishing-URL-Detection
```

Install the required libraries:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn shap jupyter
```

Download the dataset from Kaggle and update the CSV file path in the notebook.

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open `M115_Lab1_Phishing_URL_Detection.ipynb` and execute the cells.

## 12. Conclusion

This project demonstrates how Machine Learning can be applied to phishing URL detection.

By combining Exploratory Data Analysis, Logistic Regression, regularization techniques, and SHAP explainability, the project provides both predictive results and insights into the factors influencing classification decisions.

The threshold analysis further highlights the importance of balancing phishing detection performance with false-positive risks in cybersecurity operations.

Overall, this work illustrates how explainable Machine Learning can contribute to phishing detection and support security analysis in a SOC environment.



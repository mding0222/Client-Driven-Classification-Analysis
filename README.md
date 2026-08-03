# Client-Driven Classification Analysis

## Overview

This project demonstrates an end-to-end machine-learning classification workflow designed around clearly defined client requirements.

Rather than selecting a model based only on overall accuracy, the analysis focuses on the practical consequences of different classification errors and uses those requirements to guide metric selection, model optimisation and final model selection.

The workflow covers data validation, preprocessing, baseline modelling, model comparison, hyperparameter tuning and evaluation on an independent test set.

---

## Project Objective

The project uses numerical features derived from cell samples to classify observations as **malignant** or **benign**.

Two performance requirements were defined:

- Detect at least **90% of malignant cases**.
- Keep the false-positive rate for benign cases below **20%**.

Because the consequences of false negatives and false positives are different, the project treats model selection as a requirement-driven decision rather than simply maximising accuracy.

---

## Analytical Workflow

The analysis follows six main stages:

1. **Data validation** — identify inconsistent labels, invalid values and missing data.
2. **Data preparation** — clean the data and create stratified training, validation and test sets.
3. **Baseline modelling** — establish reference performance before optimisation.
4. **Model comparison** — compare SGD, SVM and Random Forest classifiers.
5. **Hyperparameter optimisation** — tune candidate models using the metric most relevant to the client requirement.
6. **Final evaluation** — assess the selected model on an independent test set and interpret its classification behaviour.

---

## Data Quality & Preprocessing

Initial exploration identified several data-quality issues, including inconsistent class labels, incorrect data types and physically invalid values.

The preprocessing workflow included:

- correcting inconsistent labels;
- converting incorrectly stored numerical values;
- identifying invalid measurements;
- handling missing values;
- standardising numerical features;
- using pipelines to reduce the risk of data leakage;
- applying stratified train, validation and test splits.

This step highlights an important part of the workflow: model performance depends on the quality and consistency of the underlying data.

---

## Model Development

The following classification approaches were evaluated:

- **SGD Classifier**
- **Support Vector Machine (SVM)**
- **Random Forest Classifier**

A random-prediction baseline was also used as a reference.

Model performance was assessed using several metrics:

- Accuracy
- Balanced Accuracy
- Recall
- Precision
- AUC
- F1-score
- F-beta scores

### Why Recall?

**Recall was selected as the primary optimisation metric** because the client requirement placed particular importance on correctly identifying malignant cases.

This demonstrates an important principle of applied analytics: the most appropriate evaluation metric depends on the problem being solved, not simply on which metric gives the largest number.

---

## Final Model

After hyperparameter optimisation and model comparison, the **SGD Classifier** was selected as the final model.

The final test-set performance was approximately:

| Metric | Result |
|---|---:|
| Accuracy | 0.94 |
| Recall | 0.90 |
| Precision | 0.90 |
| AUC | 0.93 |
| F1-score | 0.90 |

The model achieved the required malignant-case detection rate while keeping false positives within the defined acceptable range.

### Final Confusion Matrix

<p align="center">
  <img src="images/final_confusion_matrix.png" width="55%" alt="Final Model Confusion Matrix">
</p>

The confusion matrix provides a more practical view of model performance than accuracy alone by showing the balance between false negatives and false positives.

---

## Feature Discrimination

To better understand which variables most clearly distinguish the two classes, individual features were compared using absolute T-scores.

The four strongest individual features were:

- **mean concave points**
- **mean perimeter**
- **mean radius**
- **mean area**

### Most Discriminative Features

<p align="center">
  <img src="images/feature_discrimination.png" width="65%" alt="Most Discriminative Features">
</p>

Feature-level analysis provides additional insight into the structure of the dataset and helps explain which measurements contribute most strongly to class separation.

---

## Decision Boundary Analysis

Decision boundaries were visualised using combinations of the most discriminative features.

<p align="center">
  <img src="images/decision_boundaries.png" width="80%" alt="Classification Decision Boundaries">
</p>

These visualisations provide an interpretable view of how the selected classifier separates malignant and benign observations across different feature combinations.

---

## Key Findings

- Data-quality validation is an essential step before model development.
- Accuracy alone is not sufficient when different classification errors have different consequences.
- Evaluation metrics should reflect the practical requirements of the problem.
- Recall was the most relevant optimisation metric for the defined client objective.
- The optimised SGD classifier provided the best fit to the defined performance requirements among the tested models.
- Feature analysis and decision-boundary visualisation provide useful interpretation beyond aggregate performance metrics.

---

## Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- Jupyter Notebook

---

## Repository Structure

~~~text
client-driven-classification-analysis/
│
├── README.md
│
├── notebooks/
│   └── 01_client_driven_classification.ipynb
│
└── images/
    ├── final_confusion_matrix.png
    ├── feature_discrimination.png
    └── decision_boundaries.png
~~~

---

## How to Explore the Project

Open the notebook:

~~~text
notebooks/01_client_driven_classification.ipynb
~~~

The notebook contains the complete analytical workflow, including data cleaning, preprocessing, model development, optimisation, evaluation and interpretation.

The main Python libraries used are **Pandas, NumPy, Matplotlib, Seaborn and scikit-learn**.

---

## Limitations & Future Improvements

The dataset used in this project is relatively small, which limits how confidently the results can be generalised.

Potential improvements include:

- evaluation on a larger dataset;
- repeated or nested cross-validation;
- probability-threshold optimisation;
- further feature-selection analysis;
- comparison with additional ensemble models;
- improved model interpretability.

---

## Note

This repository is a cleaned and reorganised portfolio version of work originally developed during postgraduate study.

The purpose of the project is to demonstrate data-quality analysis, machine-learning workflow, model evaluation and requirement-driven decision making.

It is an educational analytics project and is **not intended for clinical or medical use**.

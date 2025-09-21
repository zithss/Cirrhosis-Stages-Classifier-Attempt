# Cirrhosis Stages — Data Analysis & ML Notebook

## Project overview

Analysis and machine learning on a cirrhosis stages dataset. The notebook covers data loading, cleaning, EDA, basic feature inspection, and model development using tree-based classifiers (RandomForest and XGBoost). Focus is on exploration and learning; results show room for improvement due to missing data and class imbalance.

## Data (columns)

**Numerical:**
`ID, Bilirubin, Cholesterol, Albumin, Copper, Alkaline Phospatase (U/L), SGOT, Tryglicerides, Platelets, Prothrombin`

**Categorical / Metadata:**
`Registration Date, Drug, Birth Date, Gender, Ascites, Hepatomegaly, Edema, Stage` (target)

## Missing data (summary)

* Columns with **≥ 20% missing**: `Drug, Ascites, Hepatomegaly, Copper, Alkaline Phospatase (U/L), SGOT, Tryglicerides (>30%)`
* Columns with **< 5% missing**: `Platelets, Prothrombin`
  (These missingness patterns strongly affect model quality and require careful handling.)

## EDA (what was done)

* Distribution plots (boxplots) for numerical features.
* Barplots for categorical features (counts per category).
* Class balance inspection for the `Stage` target.

## Preprocessing

* Basic imputation/cleanup (noting many features require better domain-informed imputation).
* Encoding of categorical variables.
* Train / validation / test split (chronological or random depending on notebook cells).
* Feature selection and simple pipelines used before modeling.

## Models trained

* **RandomForestClassifier** (baseline)
* **XGBClassifier** (baseline + hyperparameter-tuned variant)

### Reported results

* **RandomForestClassifier**

  * Accuracy: **0.4699**
  * F1 (weighted): **0.4416**
* **XGBClassifier**

  * Accuracy: **0.4940**
  * F1 (weighted): **0.4652**

> XGBoost gives a small improvement, but both models underperform — largely due to missing data and class imbalance.

## Key conclusions

* Models struggled with class imbalance and noisy / incomplete features.
* XGBoost performed slightly better than RandomForest but overall predictive power is limited.
* Better imputation strategies and addressing class imbalance are required for meaningful improvement.

## Suggested next steps (practical)

1. **Imputation:** use domain-aware imputation, k-NN imputation, or multiple imputation rather than simple mean/median.
2. **Class imbalance:** try stratified resampling, class weights, SMOTE/ADASYN, or focal loss for better class-sensitive learning.
3. **Feature engineering:** add feature interactions meaningful to clinicians.
4. **Modeling:** calibrate probabilities, try stacked ensembles, and tune with cross-validated grid/random/Optuna searches.
5. **Evaluation:** use per-class recall/precision, confusion matrix, and macro-F1 in addition to weighted metrics to understand minority-class performance.
6. **Expert input:** consult domain experts for meaningful imputation and feature importance interpretation.

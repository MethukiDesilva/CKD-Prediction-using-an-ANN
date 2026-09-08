# CKD-Prediction-using-an-ANN
This project builds, trains, and evaluates an Artificial Neural Network (ANN) to predict Chronic Kidney Disease from patient lab values.
# Chronic Kidney Disease (CKD) Prediction using an ANN

This project builds, trains, and evaluates an Artificial Neural Network (ANN) to predict Chronic Kidney Disease from patient lab values. K-Nearest Neighbours (KNN) and Logistic Regression are included as baseline models, to check whether the ANN's performance reflects genuine predictive signal in the data rather than model-specific overfitting.

## Dataset

- File: `new_model.csv`
- 400 patient records, 13 features + 1 target column (`Class`)
- Features: `Bp`, `Sg`, `Al`, `Su`, `Rbc`, `Bu`, `Sc`, `Sod`, `Pot`, `Hemo`, `Wbcc`, `Rbcc`, `Htn`
- Target: `Class` (1 = CKD, 0 = No CKD)
- No missing values, no duplicated rows
- Class balance: 62.5% CKD / 37.5% No CKD (moderately imbalanced)

## Project Structure

1. **Imports and data loading**
2. **Exploratory Data Analysis (EDA)** — missing values, duplicates, class distribution
3. **Data preprocessing** — feature/target split, stratified train/validation/test split, feature scaling
4. **Baseline models** — KNN and Logistic Regression
5. **ANN architecture and training** — with EarlyStopping
6. **Evaluation** — accuracy, precision, recall, F1, confusion matrix
7. **Model comparison** — ANN vs. baselines
8. **Discussion and limitations**

## Methodology

- Data split 70/15/15 into train (280), validation (60), and test (60) sets, stratified on `Class`.
- `StandardScaler` is fit only on the training set and applied to validation/test — avoids data leakage.
- ANN architecture: `Dense(128, relu) → Dense(64, relu) → Dense(1, sigmoid)`, compiled with Adam and binary cross-entropy.
- `EarlyStopping` monitors validation loss (`patience=5`, `restore_best_weights=True`) to guard against overfitting given the small dataset.
- `random_state=42` / `np.random.seed(42)` / `tf.random.set_seed(42)` used throughout for reproducibility.

## Results

| Model               | Test Accuracy |
|---------------------|---------------|
| KNN (k=5)            | 0.983         |
| Logistic Regression  | 0.983         |
| ANN                   | 0.967         |


All three models performed very similarly, the CKD and non-CKD groups appear to be clearly separated by important lab values such as serum creatinine, blood urea, and haemoglobin. 

## Requirements

```
pandas
numpy
matplotlib
seaborn
scikit-learn
tensorflow
```

## How to Run

1. Place `new_model.csv` in the same directory as the notebook.
2. Install dependencies: `pip install pandas numpy matplotlib seaborn scikit-learn tensorflow`
3. Run all cells top-to-bottom in Jupyter.

## Author

Methuki De Silva

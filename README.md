# NBA_Predictions

## Introduction
This repository includes a script to predict the **missing fifth home player** in NBA lineups. Due to **RAM constraints**, this version uses **only 2007–2009** data and trains a **RandomForestClassifier** with **100 estimators**. These limitations may result in **lower test accuracy** than if a larger dataset and/or more robust model configurations were used.

## File Overview
1. **Matchup-metadata.xlsx**  
   - Excel file specifying allowed features for the model.
2. **matchups-20YY.csv**  
   - Multiple CSVs for training data (e.g., 2007, 2008, 2009).  
3. **NBA_test.csv**  
   - Test data with 4 home players (missing the 5th) and 5 away players, plus other features.
4. **NBA_test_labels.csv**  
   - Ground truth of removed fifth players for the test set.

## How to Run
1. **Install Dependencies**  
   - Python 3+  
   - Libraries: `pandas`, `numpy`, `scikit-learn`, `openpyxl`
     ```bash
     pip install pandas numpy scikit-learn openpyxl
     ```
2. **Check File Paths**  
   - Ensure `metadata_file`, `csv_files`, and test file paths (`NBA_test.csv`, `NBA_test_labels.csv`) are correct.
3. **Execute the Script**  
   - Run the entire script (e.g., in a Jupyter Notebook or `.py` file).  
   - The code will print:
     - **Metadata & Feature Info**  
     - **Training/Validation Data Shapes**  
     - **Validation Accuracy & Classification Report**  
     - **Test Accuracy & Classification Report** (if the ground truth column is recognized)  
     - **Matches per Year** in the test data  
     - **Top 10 Feature Importances**
4. **Output**  
   - A CSV file named `NBA_predictions.csv` containing `Game_ID` (if available), `Home_Team` (if available), and `Fifth_Player` (the predicted missing player).

## Result Summary
- **Training Data Used**: 2007–2009 due to memory constraints.  
- **Model**: RandomForest with only **100 estimators** to limit RAM usage.  
- **Validation Accuracy**: Printed at the end of training (varies by run).  
- **Test Accuracy**: Tends to be **relatively low** (single-digit or teens), partly because we used fewer years of data and a smaller model size.  
- **Feature Importances**: Displayed in the console; they highlight which features the model relies on the most.

## Code Sections (Brief Overview)
1. **Imports & Globals**  
   - Loads libraries, sets `RANDOM_STATE`.
2. **Metadata Loading**  
   - Reads `Matchup-metadata.xlsx` and determines **allowed_features**.
3. **Training Data Loading**  
   - Merges multiple annual CSVs (2007–2009 here).
4. **Target Determination**  
   - Identifies the missing fifth player column (e.g., `home_4`).
5. **Data Cleaning & Encoding**  
   - Fills missing values and applies `LabelEncoder` to categorical columns.
6. **Model Training**  
   - Splits data into train/validation sets and fits a RandomForest with 100 trees.
7. **Test Data Preparation & Prediction**  
   - Cleans, encodes, and predicts the missing player in `NBA_test.csv`.
8. **Evaluation**  
   - Compares predictions to `NBA_test_labels.csv` (via `removed_value` or similar).  
   - Prints final test accuracy, classification report, and test data stats.

## Limitations and Next Steps
- **Memory Constraints**: We only used ~3 years of data (2007–2009) to prevent crashes.  
- **Accuracy**: May be improved by training on **more years**, increasing **n_estimators**, or using a different model (e.g., CatBoost or LightGBM).  
- **Feature Engineering**: Additional player performance stats or advanced transformations might boost predictive power.

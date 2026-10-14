# Power System Load Type Prediction

## Project objective
Train a multiclass classifier to predict `Load_Type` (`Light_Load`, `Medium_Load`, `Maximum_Load`) from historical power-system measurements.

## Folder structure
```text
power_load_prediction/
├── README.md
├── requirements.txt
├── data/
│   ├── raw/
│   │   ├── load_data.csv
│   │   └── Problem statement.docx
│   └── processed/
│       └── load_data_timestamp_cleaned.csv
├── notebooks/
│   └── power_load_type_prediction.ipynb
├── reports/
│   └── results_summary.md
└── src/
    └── README.md
```

## Run the notebook
Recommended: Python 3.10–3.13 in a virtual environment.

```bash
python -m venv .venv
source .venv/bin/activate        # macOS/Linux
# .venv\\Scripts\\activate   # Windows
python -m pip install --upgrade pip
pip install -r requirements.txt
jupyter notebook notebooks/power_load_type_prediction.ipynb
```

Run all cells from top to bottom. The notebook searches for the CSV relative to the project root or notebook directory.

## Methodology
- Parse the source timestamp and sort observations chronologically.
- Remove rows with unparseable timestamps and keep the first row for any duplicate timestamp.
- Retain missing feature values until model preprocessing; median imputation is fitted on the training set only.
- Engineer calendar fields and cyclical hour/month features.
- Use the final calendar month in the data as the test set; all earlier months are training data.
- Compare Logistic Regression and Random Forest.
- Evaluate with accuracy, macro precision/recall/F1, weighted F1, a classification report, and a confusion matrix.

## Important notes
- The provided CSV is the source of truth. The raw file is preserved unchanged.
- The processed CSV only parses the timestamp and removes duplicate timestamps; it does not impute values or remove outliers.
- The final month is determined from the data rather than hard-coded.
- Metrics shown in `reports/results_summary.md` are the observed result for this supplied dataset and this specific chronological split. They should not be interpreted as a guarantee of future performance.

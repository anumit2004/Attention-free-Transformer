# AFT_FULL

This folder contains the full, stabilized Attention-free Transformer (AFT) experiment workflow and its hyperparameter tuning records.

## Contents

- `AFT_FULL_Stabilised.ipynb`
  - Main notebook for the full AFT pipeline.
  - Includes model setup, training flow, and evaluation steps for the stabilized experiment version.

- `Hyperparameter_Tuning_results_aft_full_wiki.xlsx`
  - Central spreadsheet containing hyperparameter tuning results for the full AFT experiments.
  - Use this file to compare configurations and identify best-performing runs.

## How to Use This Folder

1. Open `AFT_FULL_Stabilised.ipynb` to run or review the full experiment workflow.
2. Check `Hyperparameter_Tuning_results_aft_full_wiki.xlsx` to inspect the outcomes of tuning runs.
3. Use the workbook results to select or justify the final hyperparameter settings used in the notebook.

## Recommended Tracking Fields in the Excel Workbook

Keep each run as one row with fields such as:

- Run ID
- Learning Rate
- Batch Size
- Epochs
- Dropout
- Optimizer
- Validation Metric(s)
- Test Metric(s)
- Notes

This keeps tuning reproducible and makes it easy to compare results across experiments.

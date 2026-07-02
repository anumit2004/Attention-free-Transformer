# Attention-free Transformer

This repository contains notebook-based experiments for the Attention-free Transformer (AFT), including a full training/tuning workflow under `AFT_FULL`.

## Repository Overview

- `AFT_LOCAL.ipynb`: Local AFT experimentation notebook.
- `aft_simple.ipynb`: Simplified AFT implementation/experiments.
- `aft-coding.ipynb`: Coding and exploratory notebook work.
- `AFT_FULL/`: Full AFT workflow and tuning artifacts.

## AFT_FULL Overview

The `AFT_FULL` folder contains the complete, stabilized workflow for full-scale AFT experiments:

- `AFT_FULL/AFT_FULL_Stabilised.ipynb`: Main notebook for the stabilized full AFT setup (modeling, training, and evaluation workflow).

## Hyperparameter Tuning Data (Excel)

All collected hyperparameter tuning results for the full AFT setup are stored in:

- `AFT_FULL/Hyperparameter_Tuning_results_aft_full_wiki.xlsx`

This Excel file is intended to be the central record of tuning runs and outcomes. Use it to:

- Track tested hyperparameter combinations.
- Compare run performance across settings.
- Identify the best-performing configuration(s).

## Notes

- Notebooks are the primary source of implementation and experiment flow.
- The Excel workbook is the primary tabular log for hyperparameter search results in `AFT_FULL`.

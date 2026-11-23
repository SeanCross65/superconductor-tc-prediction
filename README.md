# Superconductor Critical Temperature Analysis

Group project by Sean, Ewan & Farouk.

## Overview

This project investigates what physicochemical properties drive high critical temperature (Tc) in superconductors, and whether a material can be classified as a "practical" superconductor (Tc above 77 K, the boiling point of liquid nitrogen) from its composition alone.

Materials with Tc above 77 K can be cooled with liquid nitrogen instead of liquid helium, making them far cheaper and more practical for real-world applications (MRI, power transmission, quantum computing).

## Research Questions

1. What physicochemical properties actually drive high critical temperature?
2. Can a material be classified as a "practical" superconductor (Tc > 77 K) from its composition alone?

## Key Results

- **Regression:** Random Forest performed best (RMSE 9.36 K, R² 0.926), almost halving the error of linear regression (RMSE 17.66 K).
- **Feature importance:** grouped by property, thermal conductivity and valence matter most.
- **Classification (Tc > 77 K):** Random Forest and Gradient Boosting were tied as the best classifiers (F1 ≈ 0.85).
- **Validation:** with grouped cross-validation (keeping very similar materials together), RMSE rises from about 9.3 K to about 13.4 K, so the random-split score is somewhat optimistic.

All figures are saved in [`results/figures/`](results/figures/).

## Dataset

- **Name:** Superconductor Dataset (Kaggle mirror of the UCI "Superconductivty Data" dataset)
- **Source:** [kaggle.com/datasets/munumbutt/superconductor-dataset](https://www.kaggle.com/datasets/munumbutt/superconductor-dataset) (original: [UCI ML Repository](https://archive.ics.uci.edu/dataset/464/superconductivty+data))
- **Size:** 21,263 superconductors, 81 physicochemical features, with critical temperature as the target variable
- **Citation:** Hamidieh, K. (2018). A data-driven statistical model for predicting the critical temperature of a superconductor. *Computational Materials Science*, 154, 346–354.

`train.csv` is downloaded automatically from Kaggle via `kagglehub` when the notebook runs. `unique_m.csv` (element composition of each material, used to identify cuprates) is included in `data/`; if it's missing, the notebook re-downloads it from UCI.

The full dataset reference, research question rationale and ethics checklist are in [`notebooks/00_week2_RQ_data_ethics.ipynb`](notebooks/00_week2_RQ_data_ethics.ipynb).

## Repo Structure

```
.
├── data/
│   └── unique_m.csv                     # Element composition per material (from UCI)
├── notebooks/
│   ├── 00_week2_RQ_data_ethics.ipynb    # Research questions, dataset reference, ethics checklist
│   └── SuperConductivity.ipynb          # Main analysis: EDA, regression, feature importance, classification, validation
├── results/
│   └── figures/                         # Plots exported from the main notebook
├── slides/                              # Presentation materials
├── .gitignore
├── README.md
└── requirements.txt
```

## Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/SeanCross65/superconductor-tc-prediction.git
   cd superconductor-tc-prediction
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Open and run the main notebook from the `notebooks/` folder:
   ```bash
   jupyter notebook notebooks/SuperConductivity.ipynb
   ```

## Notes on Ethics

This dataset contains no personal or human-subject data. It describes chemical compositions and physical properties of materials, not people. The main ethical consideration is publication bias in the underlying literature, which may over-represent already well-studied superconductor families and under-represent negative results or unpublished materials. See the ethics checklist notebook for full details.

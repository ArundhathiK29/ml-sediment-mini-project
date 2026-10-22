# Predicting Sediment Particle Size Distributions (ML Mini-Project, UE24CS352A)

Random Forest and SVR regression predicting median particle diameter (d50) and PSD variance
from 8 water-quality / hydrodynamic features, based on Egan, "Machine learning for predicting
sediment particle size distributions". The data is synthetic (generated inside the notebook).

## Repository layout
    ml_mini_project.ipynb          main notebook (run top to bottom)
    requirements.txt               Python dependencies
    data/sediment_particle_dataset.csv   generated dataset (seed 42, 5000 rows)
    results/                       created when the notebook runs (metrics, predictions, models)
    report/ML_Mini_Project_Report.pdf    2-page write-up

## Setup and run
    pip install -r requirements.txt
    jupyter notebook ml_mini_project.ipynb

Run all cells top to bottom (Kernel > Restart & Run All). No Colab or manual upload needed.
The notebook regenerates `data/` and `results/` itself, and all random seeds are fixed (42).

## Method summary
1. Generate synthetic data (8 features, 2 targets) and explore it.
2. 80/20 train/test split; test set used once at the end.
3. Random Forest importance (impurity + permutation, per target) -> keep top 4 features.
4. Tune RF trees with OOB score and SVR (C, epsilon, gamma) with 3-fold CV.
5. Evaluate with R2, MAE, RMSE; 5-fold CV check; compare to the noise ceiling.

## Key results (test set)
| Target | RF (top-4) R2 | SVR (top-4) R2 | Noise ceiling |
|---|---|---|---|
| d50 | 0.909 | 0.921 | 0.930 |
| psd_variance | 0.936 | 0.948 | 0.958 |

Note: the data is synthetic, so these scores show the pipeline works, not that it predicts real flocculation.

# Computational Analysis of DnaG Primase Inhibitors

This repository contains the computational workflow used to identify key molecular descriptors that distinguish **non-inhibitors**, **specific inhibitors**, and **broad-spectrum inhibitors** of bacterial DnaG primase.

## Repository Contents

- **`DnaG Inhibitors.ipynb`**  
  Main Jupyter notebook containing the full analysis pipeline, including:
  - Feature preprocessing and selection (Mutual Information, mRMR)
  - Model training (Lasso, SVM, Decision Tree, XGBoost)
  - SHAP analysis (multiclass and One-vs-Rest)
  - Aggregation of feature importance across models
  - Directionality analysis (feature value vs. contribution)
  - Visualization of results (Figures 5a, 5b, and supplementary figures)

- **`molecule_features_specific-broad_inhibition-non-inhibition.csv`**  
  Dataset containing:
  - RDKit molecular descriptors (217 features per molecule)
  - Class labels:
    - `Non` – non-inhibitors  
    - `Specific` – inhibitors active against ≤2 DnaG primases  
    - `Broad` – inhibitors active against >2 DnaG primases  

## Overview of the Workflow

1. **Feature Extraction**  
   217 RDKit descriptors were computed for each molecule.

2. **Feature Selection**
   - Removal of highly correlated descriptors (threshold > 0.9)
   - Ranking by Mutual Information (MI)
   - Selection of top 25 descriptors using mRMR (Minimum Redundancy Maximum Relevance)

3. **Model Training**
   Four classification models were trained:
   - Lasso (L1-regularized logistic regression)
   - Linear Support Vector Machine (SVM)
   - Decision Tree
   - XGBoost

4. **Model Interpretation**
   - SHAP (SHapley Additive exPlanations) used for multiclass interpretation
   - One-vs-Rest (OvR) SHAP used for binary class-specific interpretation
   - Feature importance aggregated across models

5. **Directionality Analysis**
   - Correlation between feature values and SHAP values used to determine:
     - Whether high or low descriptor values favor a given class
   - Results aggregated across models and methods (SHAP + OvR)

6. **Visualization**
   - Feature importance plots (mean normalized SHAP values)
   - Directionality plots (correlation-based, SHAP-inspired visualization)
   - Supplementary figures for model performance and interpretability

## Key Outputs

- Identification of key descriptors contributing to classification
- Consensus feature importance across multiple models
- Directionality of descriptor contributions (high vs. low values)
- Interpretable rules from decision tree model

## Dependencies

The analysis was performed using the following Python libraries:

- `numpy`
- `pandas`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `scipy`
- `xgboost`
- `shap`
- `mpl_toolkits.mplot3d`

You can install all dependencies via pip:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn scipy xgboost shap
```

## Citation

If you use this repository, data, or methodology in your work, please cite:

Bhattarai, S.; Trachtenberg, A.; Tiwari V. S.; Akabayov B. (2026). Exploring Broad-Spectrum Inhibition: A Comparative Study on the
Discovery of Indole-Based DnaG Inhibitors Across Bacterial Species.

## License

This project is released under the MIT License.

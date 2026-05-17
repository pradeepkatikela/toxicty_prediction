# Toxicity Prediction with XGBoost

## Project Overview
This notebook demonstrates a machine learning workflow for predicting chemical toxicity based on molecular properties. It utilizes the Tox21 dataset, which contains toxicity screening data for various compounds. The core of the prediction model is an XGBoost Classifier, augmented with molecular descriptors and atom counts as features.

## Dataset
The dataset used is `tox21.csv`, which contains information about chemical compounds, their SMILES strings, and their activity across various toxicity assays (NR-AR, NR-AR-LBD, etc.). A `toxicity_label` is derived from these assay results to indicate whether a compound is considered toxic (1) or non-toxic (0).

## Dependencies
To run this notebook, you need the following Python libraries:
- `pandas`
- `numpy`
- `xgboost`
- `scikit-learn` (for `model_selection`, `metrics`, `impute`)
- `pubchempy`
- `rdkit`
- `matplotlib`
- `seaborn`

These can be installed using pip:
```bash
pip install pandas numpy xgboost scikit-learn pubchempy rdkit matplotlib seaborn
```
(Note: `rdkit` might require specific installation steps depending on your environment. The `%pip install rdkit` command in the notebook usually works well in Colab).

## Methodology
1.  **Data Loading**: The `tox21.csv` file is loaded into a pandas DataFrame.
2.  **Toxicity Labeling**: A binary `toxicity_label` is created. A compound is labeled `1` (toxic) if it shows activity (value `1`) in *any* of the specified toxicity columns, and `0` (non-toxic) if it shows inactivity (value `0`) in *any* of the columns and no activity in any other. Rows with ambiguous or entirely missing labels are dropped.
3.  **Feature Engineering (RDKit Descriptors)**:
    *   **Molecular Descriptors**: For each compound's SMILES string, molecular weight (MolWt), number of hydrogen bond donors (NumHDonors), hydrogen bond acceptors (NumHAcceptors), octanol-water partition coefficient (MolLogP), and topological polar surface area (TPSA) are calculated using RDKit's `Chem.Descriptors` module.
    *   **Atom Counts**: Counts of Nitrogen (N), Oxygen (O), Halogens (Cl, Br, F, I), and Aromatic atoms are extracted.
4.  **Feature Combination**: The generated molecular descriptors and atom counts are combined with the original toxicity assay columns to form the feature matrix `X_extra`.
5.  **Missing Value Imputation**: `SimpleImputer` with a 'most_frequent' strategy is used to handle any remaining missing values in the feature set.
6.  **Data Splitting**: The dataset is split into training and testing sets (80% train, 20% test) using `train_test_split` with stratification to maintain the class distribution.
7.  **Noise Introduction (Optional)**: 5% random noise is intentionally introduced into the `y_train` labels to simulate real-world data challenges.
8.  **Model Training**: An XGBoost Classifier (`xgb.XGBClassifier`) is trained on the noisy training data.
9.  **Model Evaluation**: The trained model's performance is evaluated on the test set using:
    *   Accuracy Score
    *   Classification Report (precision, recall, f1-score)
    *   Confusion Matrix
    *   ROC Curve and Area Under the Curve (AUC)
10. **Compound Name Retrieval**: PubChemPy is used to fetch common names for example toxic and non-toxic compounds based on their SMILES strings.
11. **Feature Importance Visualization**: A bar plot visualizes the top 8 most important features as determined by the XGBoost model.

## Results and Findings
The XGBoost model achieved a promising accuracy of **92.53%** on the test set. The classification report and confusion matrix provide a detailed breakdown of precision, recall, and F1-score for both 'Non-Toxic' and 'Toxic' classes. The ROC AUC score further confirms the model's ability to distinguish between the two classes.

Key observations from the feature importance plot suggest that several original toxicity assays (e.g., `NR-ER`, `SR-ATAD5`) along with molecular descriptors like `MolWt` and `LogP`, and atom counts such as `Aromatic_count` and `O_count`, are crucial for predicting toxicity.

The examples of predicted toxic and non-toxic compounds, along with their PubChem names, offer qualitative insights into the model's predictions.

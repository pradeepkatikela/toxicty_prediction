# Toxicity Prediction with XGBoost

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Jupyter Notebook](https://img.shields.io/badge/Notebook-Jupyter-orange.svg)](https://jupyter.org/)

A machine learning project for predicting chemical toxicity based on molecular properties using XGBoost and RDKit molecular descriptors on the Tox21 dataset.

## 📋 Project Overview

This notebook demonstrates a complete machine learning workflow for predicting chemical toxicity. It utilizes the Tox21 dataset, which contains toxicity screening data for various chemical compounds across multiple toxicity assays. The project achieves **92.53% accuracy** using XGBoost with engineered molecular descriptors.

### Key Features:
- Binary classification of toxic vs. non-toxic compounds
- Feature engineering using RDKit molecular descriptors
- Comprehensive model evaluation with ROC-AUC analysis
- Feature importance visualization
- Compound name retrieval using PubChemPy

## 📊 Dataset

The project uses the **Tox21 dataset** (`tox21.csv`) containing:
- SMILES strings for chemical compounds
- Activity data across multiple toxicity assays (NR-AR, NR-AR-LBD, NR-AhR, NR-Aromatase, etc.)
- Binary toxicity labels indicating compound activity

A compound is labeled as **toxic (1)** if it shows activity in any of the specified toxicity columns, otherwise **non-toxic (0)**.

## 🚀 Getting Started

### Prerequisites
- Python 3.8 or higher
- pip or conda package manager
- Jupyter Notebook or JupyterLab

### Installation

1. **Clone the repository:**
```bash
git clone https://github.com/pradeepkatikela/toxicty_prediction.git
cd toxicty_prediction
```

2. **Install dependencies:**

**Option 1: Using pip**
```bash
pip install -r requirements.txt
```

**Option 2: Manual installation**
```bash
pip install pandas numpy xgboost scikit-learn pubchempy rdkit matplotlib seaborn
```

> **Note:** `rdkit` might require specific installation steps depending on your environment. For Google Colab, use `%pip install rdkit` directly in a cell.

### Running the Project

1. **Start Jupyter Notebook:**
```bash
jupyter notebook
```

2. **Open the notebook:**
   - Open `toxicity_prediction.ipynb` in your browser
   - Run cells sequentially from top to bottom
   - Ensure the `tox21.csv` dataset file is in the same directory

## 🔧 Dependencies

| Package | Purpose |
|---------|---------|
| `pandas` | Data manipulation and analysis |
| `numpy` | Numerical computing |
| `xgboost` | XGBoost classifier model |
| `scikit-learn` | ML utilities (train/test split, metrics, imputation) |
| `pubchempy` | Fetch compound names from PubChem |
| `rdkit` | Molecular descriptor calculation |
| `matplotlib` | Data visualization |
| `seaborn` | Statistical data visualization |

## 🔬 Methodology

### 1. **Data Loading**
   - Load the `tox21.csv` file into a pandas DataFrame

### 2. **Toxicity Labeling**
   - Create binary `toxicity_label`: 1 if compound is active in any assay, 0 otherwise

### 3. **Feature Engineering**
   - **Molecular Descriptors:**
     - Molecular Weight (MolWt)
     - Hydrogen Bond Donors (NumHDonors)
     - Hydrogen Bond Acceptors (NumHAcceptors)
     - LogP (Octanol-water partition coefficient)
     - Number of Rotatable Bonds
   - **Atom Counts:** N, O, Halogens (Cl, Br, F, I), Aromatic atoms

### 4. **Data Preprocessing**
   - Combine molecular descriptors with original toxicity assay columns
   - Handle missing values using SimpleImputer (most_frequent strategy)
   - Split data: 80% training, 20% testing (stratified)

### 5. **Model Training**
   - Introduce 5% random noise in training labels (simulates real-world challenges)
   - Train XGBoost Classifier on noisy training data

### 6. **Model Evaluation**
   - Accuracy Score
   - Classification Report (Precision, Recall, F1-Score)
   - Confusion Matrix
   - ROC Curve and AUC

### 7. **Visualization**
   - Feature Importance plot (top 8 features)
   - ROC curve visualization
   - Example predictions with PubChem compound names

## 📈 Results and Findings

### Model Performance
- **Accuracy:** 92.53% on test set
- **Key Features:** NR-ER, SR-ATAD5, MolWt, LogP, atom counts

### Key Observations
- Original toxicity assays are strong predictors of overall toxicity
- Molecular descriptors (MolWt, LogP) provide valuable signal
- Atom composition features contribute to model predictions
- The model generalizes well with stratified train-test split

### Insights
- Example predictions demonstrate the model's ability to identify toxic and non-toxic compounds
- PubChem compound name retrieval provides qualitative validation of predictions

## 📂 File Structure

```
toxicty_prediction/
├── README.md                      # Project documentation
├── requirements.txt               # Python dependencies
├── .gitignore                    # Git ignore file
├── toxicity_prediction.ipynb     # Main Jupyter notebook
├── tox21.csv                     # Dataset (add separately)
└── LICENSE                       # MIT License
```

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs or issues
- Suggest improvements or new features
- Submit pull requests

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Pradeep Katikela**
- GitHub: [@pradeepkatikela](https://github.com/pradeepkatikela)

## 🙏 Acknowledgments

- **Tox21 Dataset:** National Center for Advancing Translational Sciences (NCATS)
- **Libraries:** Pandas, Scikit-learn, XGBoost, RDKit, Matplotlib, Seaborn
- **Tools:** Jupyter Notebook, Python 3.8+

## 📚 References

- [Tox21 Challenge Data](https://tripod.nih.gov/tox21/challenge/)
- [XGBoost Documentation](https://xgboost.readthedocs.io/)
- [RDKit Documentation](https://www.rdkit.org/docs/)
- [Scikit-learn Documentation](https://scikit-learn.org/)

## ❓ Questions or Issues?

If you have any questions or encounter issues, please open an [issue](https://github.com/pradeepkatikela/toxicty_prediction/issues) on GitHub.

---

**Last Updated:** May 2026

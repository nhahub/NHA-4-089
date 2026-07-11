# Cancer Type Classification — TCGA Pan-Cancer Gene Expression

A complete data science pipeline that classifies cancer type from gene expression data, built across four milestones: data exploration, analysis & visualization, model development, and deployment/monitoring.

## 📋 Project Overview

This project uses the **TCGA Pan-Cancer** gene expression dataset to train and deploy a machine learning model that predicts a patient's cancer type from their gene expression profile. The pipeline covers everything from raw data cleaning to a live REST API and monitoring setup.

## 🗂️ Project Structure

```
.
├── gene_cancer_analysis_ALL_MILESTONES_COMPLETED.ipynb   # main analysis notebook
├── app.py                                                  # Streamlit app for live predictions
├── models/<version>/                                       # saved pipeline artifacts
│   ├── scaler.joblib
│   ├── variance_selector.joblib
│   ├── pca.joblib
│   ├── label_encoder.joblib
│   └── model.joblib
├── artifacts/                                              # exported cleaned dataset + copies of key artifacts
├── powerbi_export/                                         # CSV exports for Power BI dashboards
├── reports/
│   └── performance_log.csv                                 # periodic model performance snapshots
└── README.md
```

## 🔬 Methodology

### Milestone 1 — Data Collection, Exploration & Preprocessing
- Loaded and merged TCGA Pan-Cancer gene expression + phenotype data
- Explored feature distributions, missing values, and class balance
- Cleaned and structured the dataset for modeling

### Milestone 2 — Data Analysis & Visualization
- Correlation analysis and a one-way **ANOVA hypothesis test** to confirm genes are statistically associated with cancer type
- PCA-based visualizations, heatmaps, and a donut chart of class distribution
- An **interactive Plotly dashboard** for exploring patient clusters

### Milestone 3 — Predictive Model Development
- A **KMeans** unsupervised sanity check before committing to supervised learning
- Trained and tuned **Random Forest** and **SVM** classifiers
- Evaluated with cross-validation, confusion matrices, weighted F1, and multi-class **ROC-AUC**
- Selected a final model based on overall performance

### Milestone 4 — MLOps, Deployment & Monitoring
- Experiment tracking and model versioning with **MLflow**
- A `predict_cancer_type()` inference function wrapping the full pipeline (scaling → feature selection → PCA → classification)
- A **FastAPI REST API** (`/health`, `/predict`) exposing the model as a live service
- **Model monitoring**: a Population Stability Index (PSI) drift check with automated alerts
- **Periodic performance reporting**, logged to `reports/performance_log.csv`

## 🚀 Running the Notebook

```bash
pip install -r requirements.txt
jupyter notebook gene_cancer_analysis_ALL_MILESTONES_COMPLETED.ipynb
```

Run the cells top to bottom. Milestone 4 cells will save model artifacts to `models/<version>/`.

## 🌐 Running the API

The FastAPI app is defined inside the notebook (Milestone 4.3b). To serve it standalone, save that cell to `api.py` and run:

```bash
uvicorn api:app --host 0.0.0.0 --port 8000
```

Then open `http://localhost:8000/docs` for an interactive Swagger UI, or test with:

```bash
curl -X POST http://localhost:8000/predict \
  -H "Content-Type: application/json" \
  -d '{"gene_values": [0.1, 0.2, 0.3, ...]}'
```

## 🖥️ Running the Streamlit App

```bash
streamlit run app.py
```

The app loads the saved model artifacts from `models/<version>/` and lets you input or upload gene expression values to get a live prediction.

## 📊 Power BI Dashboard

Model performance and evaluation results are exported to `powerbi_export/`:
- `model_comparison.csv` — accuracy, F1, precision, recall per model
- `confusion_matrix_long.csv` — long-format confusion matrix for Matrix visuals
- `feature_importance.csv` — top PCA components by Random Forest importance


## 🛠️ Tech Stack

- **Data & ML**: pandas, numpy, scikit-learn, scipy
- **Visualization**: matplotlib, seaborn, plotly
- **MLOps**: MLflow
- **Deployment**: FastAPI, uvicorn, Streamlit
- **Reporting**: Power BI

## 📈 Monitoring & Retraining

The notebook includes a PSI-based drift monitor (`check_drift()`) that compares incoming data against the training distribution and raises an alert when drift exceeds a threshold (PSI > 0.2). Performance snapshots are logged over time to support retraining decisions.


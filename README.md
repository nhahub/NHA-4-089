# 🏥 AI-Driven Disease Diagnostic Engine (EDA & Analysis)

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-Data_Analysis-orange.svg)
![Plotly](https://img.shields.io/badge/Plotly-Interactive_Viz-brightgreen.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine_Learning-blue.svg)

## 📌 Project Overview
This project focuses on building an intelligent diagnostic engine capable of predicting potential medical conditions based on user symptoms. The project processes a large-scale healthcare dataset containing **246,000+ patient records** across **773 unique diseases** and **377 symptoms**.

The core objective is to analyze symptom-disease relationships and provide the "Top 3" potential diagnoses using statistical similarity and machine learning insights.

## 🚀 Key Features
* **Comprehensive Data Cleaning:** Handled missing values, binary encoding verification, and outlier detection using IQR.
* **Advanced EDA:** Detailed statistical analysis of disease prevalence and symptom distribution.
* **Interactive Visualizations:** Used **Plotly** and **Seaborn** to create dynamic heatmaps, correlation matrices, and PCA clusters.
* **Feature Importance:** Identified the most discriminative symptoms using **Random Forest Classifier**.
* **Dimensionality Reduction:** Visualized high-dimensional medical data in 2D using **PCA**.

## 📊 Dataset Insights
* **Records:** 246,945
* **Unique Diseases:** 773
* **Symptom Features:** 377 (Binary: 0/1)
* **Average Symptoms per Case:** ~5.33
* **Target:** Predict Top 3 conditions based on symptom input.

## 🛠️ Tech Stack
- **Languages:** Python
- **Data Manipulation:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn, Plotly Express
- **Machine Learning:** Scikit-Learn (Random Forest, PCA, Label Encoding)

## 📁 Project Structure
```text
├── Data/
│   ├── Raw_Dataset.csv          # Original data
│   └── Cleaned_Disease_Symptoms.csv # Processed binary matrix
├── Notebooks/
│   └── Disease_Analysis.ipynb   # Full EDA and Preprocessing code
├── README.md                    # Project documentation
└── requirements.txt             # Necessary Python libraries

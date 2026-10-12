# Logistics Data Preprocessing & Cleaning Pipeline

A reproducible Python data preprocessing pipeline designed for supply chain and freight logistics tracking datasets. This project focuses on handling missing telemetry, treating sensor anomalies, managing transit outliers, and normalizing operational metrics for downstream analytics.

---

## 📌 Project Overview
Logistics tracking data often suffers from human entry errors, missing timestamps, and corrupted telemetry. This project demonstrates a production-grade data cleaning workflow using **Pandas**, **NumPy**, and **Scikit-Learn**.

### Key Pipeline Features:
1. **Data Profiling & Auditing:** Automated detection of nulls, duplicates, and physical domain violations (e.g., negative transit days).
2. **Standardization:** Trimming inconsistent string padding and title-casing categorical statuses.
3. **Smart Imputation:**
   - **Mode Imputation** for missing categorical vehicle types.
   - **Median Imputation** for right-skewed numerical variables (shipping costs, transit times).
4. **Outlier Detection & Capping:** Interquartile Range (IQR) Winsorization to cap extreme fulfillment delays without discarding business volume.
5. **Feature Scaling:** Min-Max normalization of cost and distance metrics for machine learning readiness.

---

## 📂 Repository Structure

```text
├── data/
│   ├── raw_logistics_data.csv          # Simulated raw uncleaned logistics records
│   └── cleaned_logistics_data.csv      # Processed & normalized logistics dataset
├── src/
│   └── preprocess_pipeline.py          # Complete data cleaning & feature scaling script
├── notebooks/
│   └── data_cleaning_walkthrough.ipynb # Interactive EDA and pipeline execution
├── docs/
│   └── Logistics_Data_Preprocessing_Report_Week2.docx # Detailed technical report
├── requirements.txt                    # Project dependencies
└── README.md                           # Documentation & execution guide
```

---

## ⚙️ Installation & Usage

### 1. Clone the repository
```bash
git clone https://github.com/your-username/logistics-data-preprocessing.git
cd logistics-data-preprocessing
```

### 2. Set up virtual environment
```bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On Linux/macOS:
source venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Run the pipeline
```bash
python src/preprocess_pipeline.py
```

---

## 📊 Pipeline Methodology Summary

| Cleaning Stage | Technique Applied | Justification |
| :--- | :--- | :--- |
| **String Uniformity** | Whitespace stripping + Title Case | Standardizes categoricals (e.g., `' truck '` -> `'Truck'`) |
| **Domain Sanity Checks** | Filter `Distance_KM > 0` & `Transit_Days > 0` | Discards physical recording impossibilities |
| **Missing Imputation** | Mode (`Vehicle_Type`), Median (`Cost`) | Prevents distortion from right-skewed cost distributions |
| **Outlier Handling** | IQR Upper Fence Capping ($Q_3 + 1.5 \times IQR$) | Retains operational freight counts while removing skew |
| **Normalization** | Min-Max Scaler (Range [0, 1]) | Scales heterogeneous units for distance-based ML models |

---

## 🛠️ Tech Stack
- **Python 3.10+**
- **Pandas** – Data manipulation & wrangling
- **NumPy** – Numerical operations & condition vectorization
- **Scikit-Learn** – Min-Max feature normalization

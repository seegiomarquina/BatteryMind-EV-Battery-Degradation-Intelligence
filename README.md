#  BatteryMind  — EV Battery Degradation Intelligence

**An AI-powered battery intelligence system for predicting electric vehicle battery health, estimating remaining useful life, analysing degradation patterns, and identifying potential anomalies.**

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Scikit--learn-orange)
![Domain](https://img.shields.io/badge/Domain-EV%20%7C%20Energy-green)
![Dataset](https://img.shields.io/badge/Dataset-NASA-red)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

##  Project Overview

BatteryMind AI is a machine learning project designed to analyse lithium-ion battery degradation and estimate battery health throughout its lifecycle.

As electric vehicle adoption increases, understanding battery ageing becomes important for predictive maintenance, vehicle reliability, energy management, and battery lifecycle planning.

This project uses experimental lithium-ion battery ageing data from NASA to build machine learning models that analyse battery performance and degradation.

The system focuses on four major capabilities:

- **State of Health (SOH) Estimation:** Estimates battery health based on measured electrical and operational characteristics.
- **Remaining Useful Life (RUL) Prediction:** Estimates the number of remaining cycles before a battery reaches a defined end-of-life capacity threshold.
- **Degradation Analysis:** Studies how battery capacity changes across charging and discharging cycles.
- **Anomaly Detection:** Identifies unusual battery observations using an Isolation Forest model.

##  Problem Statement

Lithium-ion batteries gradually lose their capacity through repeated usage and ageing.

Without effective monitoring, battery degradation can affect electric vehicle performance, operational planning, and maintenance decisions.

BatteryMind AI explores how machine learning can transform battery performance measurements into useful predictive insights.

##  Key Features

| Feature | Description |
|---|---|
| Battery SOH Prediction | Estimates battery State of Health |
| RUL Prediction | Estimates remaining cycles until the defined EOL threshold |
| Battery Degradation | Analyses capacity fade across battery cycles |
| Anomaly Detection | Identifies potentially unusual observations |
| Model Comparison | Compares multiple regression algorithms |
| Feature Importance | Uses permutation importance to study influential features |
| Model Export | Saves trained models for future inference |

##  Dataset

**Source:** NASA Ames Prognostics Center of Excellence

**Dataset:** Li-ion Battery Aging Datasets

Official dataset page:  
https://data.nasa.gov/dataset/li-ion-battery-aging-datasets

The project uses experimental battery ageing data for cells:

- B0005
- B0006
- B0007
- B0018

The data includes battery cycle measurements, voltage, current, temperature, discharge duration, and capacity information.

The dataset contains laboratory measurements and is not a direct collection of real-world electric vehicle fleet telemetry.

### End-of-Life Reference

The project uses a capacity threshold of **1.4 Ah**, equivalent to 70% of the 2.0 Ah nominal capacity, as its research-defined end-of-life reference.

This threshold is an experimental modelling choice for this project, not a universal EV battery replacement standard.

##  Technology Stack

| Category | Tools |
|---|---|
| Programming | Python |
| Development | Google Colab |
| Data Processing | Pandas, NumPy |
| Visualisation | Matplotlib, Seaborn |
| Machine Learning | Scikit-learn |
| Models | Random Forest, Extra Trees, HistGradientBoosting |
| Anomaly Detection | Isolation Forest |
| Model Interpretation | Permutation Importance |
| Model Export | Joblib |

##  Machine Learning Workflow

1. Download and extract the NASA battery ageing dataset.
2. Load and process experimental battery measurements.
3. Extract battery-level and cycle-level features.
4. Calculate State of Health from measured discharge capacity.
5. Train and compare regression models.
6. Evaluate SOH using battery-wise GroupKFold cross-validation.
7. Construct RUL labels for batteries with an observed end-of-life threshold.
8. Evaluate RUL models using battery-wise cross-validation.
9. Apply Isolation Forest for anomaly detection.
10. Generate performance visualisations and export trained models.

### Feature Engineering

The model uses features such as:

- Cycle index
- Ambient temperature
- Mean, minimum, and maximum voltage
- Voltage standard deviation and range
- Mean current and current standard deviation
- Mean and maximum temperature
- Temperature variation
- Discharge duration

The feature set intentionally excludes `cycle_progress`, which depends on the maximum observed lifetime of a battery and could introduce information leakage.

## 📈 Model Evaluation

The project compares:

- Random Forest Regressor
- Extra Trees Regressor
- HistGradientBoosting Regressor

Evaluation metrics:

- **MAE:** Mean Absolute Error
- **RMSE:** Root Mean Squared Error
- **R²:** Coefficient of Determination

Battery-wise GroupKFold validation is used so that observations from a held-out battery are not mixed into that fold's training data.

### Results

See the following generated reports for the actual evaluation results:

- `reports/soh_model_comparison.csv`
- `reports/rul_model_comparison.csv`
- `reports/final_metrics.csv`

The reported metrics should be interpreted in the context of the small number of independent battery cells in this dataset.

##  Visual Results

The `outputs/` directory contains generated visualisations, including:

- Battery capacity degradation
- SOH trends
- Actual vs predicted SOH
- Actual vs predicted RUL
- Anomaly detection
- Feature importance
- Model residual analysis

##  Repository Structure

```text
BatteryMind-AI/
│
├── notebooks/
│   └── BatteryMind_AI_Day11.ipynb
│
├── outputs/
│   └── Model visualisations
│
├── reports/
│   └── Model evaluation and battery analysis CSV files
│
├── models/
│   └── Exported machine learning models
│
├── requirements.txt
├── .gitignore
└── README.md
```

##  How to Run

### Option 1: Google Colab

1. Clone or download this repository.
2. Open `notebooks/BatteryMind_AI_Day11.ipynb` in Google Colab.
3. Run the notebook cells in order.
4. Allow the notebook to download and process the NASA dataset.
5. Review the generated reports, visualisations, and model outputs.

### Option 2: Local Environment

Install the dependencies:

```bash
pip install -r requirements.txt
```

Open the notebook using Jupyter:

```bash
jupyter notebook
```

Run the notebook from beginning to end.

##  Future Improvements

- Validate models on additional independent battery datasets.
- Incorporate real-world EV battery management system telemetry.
- Explore time-series deep learning architectures such as LSTM and Temporal Fusion Transformers.
- Develop an interactive battery health monitoring dashboard.
- Add battery charging behaviour and operating-condition analysis.
- Deploy trained models through a FastAPI prediction service.
- Evaluate model robustness across different battery chemistries and operating environments.

## Limitations

- The NASA dataset contains a limited number of independent battery cells.
- Laboratory battery measurements may not represent real-world EV operating conditions.
- RUL estimates depend on the selected end-of-life threshold and the availability of observed end-of-life cycles.
- Anomaly detection identifies statistically unusual observations; it does not establish that a battery is defective or unsafe.
- Model performance on this dataset does not guarantee equivalent performance on commercial electric vehicle batteries.

**BatteryMind AI is an educational and research-oriented predictive modelling project. It is not a certified battery diagnostic, safety, or warranty assessment system.**

##  Author

**Aditya Dhage**

Data Science | Machine Learning | Artificial Intelligence

GitHub: https://github.com/

---

##  References

1. NASA Ames Prognostics Center of Excellence — Li-ion Battery Aging Datasets.
2. Scikit-learn documentation — https://scikit-learn.org/
3. Pandas documentation — https://pandas.pydata.org/
4. NumPy documentation — https://numpy.org/

---

 If you find this project interesting, consider starring the repository.

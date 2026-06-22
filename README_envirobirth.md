# EnviroBirth: Preterm Birth Prediction Using Environmental & Maternal Data

> **Collaborative Research | Ahsanullah University of Science and Technology (AUST)**
>
> **Authors:** Tahsin Shuborna (1st Author), Azizul Hakim (2nd Author), Namira Tasnim (3rd Author)
> **Corresponding Author:** Saha Reno
> **Institution:** Department of Computer Science and Engineering, AUST, Dhaka-1208, Bangladesh

---

## What is This Project About?

### The Problem

**Preterm birth** (delivery before 37 weeks of gestation) is the leading cause of neonatal mortality and long-term child health complications. Bangladesh records one of the world's highest preterm birth rates at **16.2%** — equivalent to 56 cases per hour.

Environmental hazards significantly worsen these risks:
- **Air pollution** linked to over 6 million premature births annually worldwide
- **Extreme heat** increases preterm birth risk by up to 26%
- **Dhaka** is one of the world's most polluted cities, with PM2.5 levels exceeding WHO guidelines by more than 10x

Despite these challenges, Bangladesh lacks data-driven predictive tools that integrate environmental exposures with maternal health data.

### What We Built

**EnviroBirth** is a machine learning framework that predicts preterm birth risk by combining:
- **Maternal health data** (gestational duration, BMI, age, education)
- **Household conditions** (cooking fuel, water source, sanitation)
- **Environmental factors** (PM2.5, PM10, NO2, SO2, CO, O3, temperature, humidity, rainfall)
- **IoT air quality monitoring** from 6 locations across Dhaka

### Why It Matters

- **First Bangladesh-specific study** integrating environmental exposures with socio-demographic factors
- **Novel dataset (PreBEnvBD)** combining national health surveys with real-time air quality and meteorological data
- **Identifies actionable risk factors** for public health intervention

---

## Key Results

### Model Performance

| Model | Accuracy | Precision | Recall | F1-Score |
|-------|----------|-----------|--------|----------|
| XGBoost | 80.89% | 94.00% | 85.00% | 89.00% |
| LightGBM | **92.19%** | 92.10% | 100% | **96.00%** |
| MLP | 82.27% | 82.20% | 81.10% | 82.01% |
| SAINT | 82.97% | 93.04% | 88.02% | 90.97% |
| TabNet | **92.29%** | 92.20% | 100% | **96.03%** |
| TabTransformer | **92.25%** | 92.00% | 100% | **96.23%** |

**Best performers:** TabNet and TabTransformer exceeded 92% accuracy, but both struggled with class imbalance (high accuracy, poor minority class detection).

**Most balanced:** LightGBM achieved 92.19% accuracy with perfect recall — most reliable for clinical use.

### Transformer Model Deep Dive

| Metric | TabNet | TabTransformer |
|--------|--------|----------------|
| Accuracy | 0.92 | 0.92 |
| ROC-AUC | 0.72 | 0.71 |
| Average Precision | 0.19 | 0.19 |
| Log Loss | 0.24 | 0.30 |
| Matthews Correlation | 0.08 | 0.04 |

**Note:** High accuracy but low AP and MCC indicate class imbalance issues — transformer models correctly predict majority class but struggle with minority (preterm) cases.

---

## Top Risk Factors Identified

| Feature | Average Importance | Relevance |
|---------|-------------------|-----------|
| **Gestation_Months** | 0.17 | **High** |
| **Cooking_Location** | 0.14 | **High** |
| **NO2** | 0.08 | **High** |
| **Mother_BMI** | 0.06 | **High** |
| **PM10** | 0.02 | Medium |
| **Has_Mosquito_Net** | 0.13 | Medium |
| **Cooking_Fuel** | 0.07 | Medium |

**Key insight:** Both maternal characteristics (gestational duration, BMI) and environmental exposures (NO2, PM10, cooking conditions) are critical predictors. This supports targeted public health interventions.

---

## The PreBEnvBD Dataset

### Data Sources

| Source | Data Type | Records |
|--------|-----------|---------|
| **Bangladesh Demographic and Health Survey (BDHS)** | Maternal, neonatal, household | 73,000 |
| **Bangladesh Meteorological Department** | Weather (rainfall, humidity, temperature) | 73,000 |
| **IoT Air Quality Monitoring** | PM2.5, PM10, CO, SO2, NO2, O3 | 6 locations in Dhaka |

### IoT Deployment Locations

Dhanmondi, Kuril Bishwa Road, Mirpur, Mohakhali, Jatrabari, Uttara

### Features (58 Total)

| Category | Examples |
|----------|----------|
| **Maternal/Neonatal** | Gestational duration, maternal age, BMI, height, weight, education, delivery type |
| **Household** | Wealth index, drinking water source, sanitation, cooking fuel, housing density |
| **Environmental** | PM2.5, PM10, CO, SO2, NO2, O3, temperature, humidity, rainfall |

---

## How It Works

```
Raw Data (BDHS + Weather + IoT) 
→ Data Preprocessing (cleaning, encoding, SMOTE)
→ Feature Engineering (58 features)
→ Model Training (6 algorithms)
→ Evaluation (accuracy, precision, recall, F1, ROC-AUC, MCC)
→ Feature Importance Analysis
→ Public Health Recommendations
```

### Preprocessing Pipeline

1. **Column standardization** — manual mapping to BDHS data dictionary
2. **Missing value imputation** — mean for numerical, mode for categorical
3. **Encoding** — label encoding for tree models, one-hot for neural networks
4. **SMOTE** — synthetic minority oversampling (training set only)
5. **Feature scaling** — StandardScaler for neural networks
6. **Train-test split** — 80/20 stratified

### Models Compared

| Type | Models |
|------|--------|
| **Tree-based Ensemble** | XGBoost, LightGBM |
| **Neural Network Baseline** | MLP |
| **Transformer Models** | SAINT, TabNet, TabTransformer |

---

## My Contribution (2nd Author)

- **Co-developed PreBEnvBD dataset** — integrated BDHS, meteorological, and IoT air quality data
- **Designed environmental feature engineering pipeline** — linked air pollution and weather data to maternal health records
- **Implemented and evaluated 6 ML/DL models** — XGBoost, LightGBM, MLP, SAINT, TabNet, TabTransformer
- **Performed feature importance analysis** — identified gestational months, cooking location, NO2, mother BMI as top predictors
- **Contributed to manuscript preparation** for journal submission

**Collaborators:** Tahsin Shuborna (1st Author), Namira Tasnim (3rd Author), Saha Reno (Corresponding Author)

---

## Repository Structure

```
envirobirth/
├── README.md              # This file
├── requirements.txt       # Python dependencies
├── src/
│   ├── preprocess.py      # Data cleaning, encoding, SMOTE
│   ├── feature_engineer.py # Environmental data integration
│   ├── train_models.py    # Train all 6 models
│   ├── evaluate.py        # Metrics, confusion matrices, curves
│   └── feature_importance.py # SHAP, permutation importance
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_model_training.ipynb
│   ├── 04_evaluation.ipynb
│   └── 05_feature_importance.ipynb
├── data/
│   ├── raw/               # BDHS, weather, IoT data (not included)
│   └── processed/         # Cleaned datasets
├── results/
│   ├── confusion_matrices/
│   ├── roc_curves/
│   ├── precision_recall/
│   └── feature_importance/
└── .gitignore
```

---

## How to Run

### Prerequisites
- Python 3.10+
- 8GB+ RAM
- GPU optional (speeds up transformer training)

### Setup
```bash
git clone https://github.com/Azizulhakim185/envirobirth.git
cd envirobirth
pip install -r requirements.txt
```

### Run Full Pipeline
```bash
python src/preprocess.py        # Clean and prepare data
python src/feature_engineer.py   # Integrate environmental features
python src/train_models.py       # Train all 6 models
python src/evaluate.py           # Generate metrics and plots
python src/feature_importance.py # Analyze top predictors
```

### Jupyter Notebooks
```bash
jupyter notebook
# Open notebooks/ folder for step-by-step exploration
```

---

## Results Summary

### Confusion Matrices

**TabNet:**
| | Predicted Term | Predicted Preterm |
|---|---------------|-------------------|
| Actual Term | 13,466 | 1 |
| Actual Preterm | 1,131 | 2 |

**TabTransformer:**
| | Predicted Term | Predicted Preterm |
|---|---------------|-------------------|
| Actual Term | 13,457 | 10 |
| Actual Preterm | 1,118 | 13 |

**Issue:** Both models show high overall accuracy but poor minority class detection (very few true preterm cases correctly identified).

### Training Curves

- **TabNet:** Stable training loss convergence, validation accuracy plateaus around 92%
- **TabTransformer:** Similar pattern with slightly higher validation variance

### ROC & Precision-Recall

- **ROC-AUC:** 0.72 (TabNet), 0.71 (TabTransformer) — moderate discriminative ability
- **Average Precision:** 0.19 for both — poor due to class imbalance
- **Matthews Correlation:** 0.08 (TabNet), 0.04 (TabTransformer) — confirms imbalance issues

---

## Key Insights

### For Public Health

| Finding | Actionable Intervention |
|---------|------------------------|
| **Gestation months** most important | Early and consistent prenatal care |
| **Cooking location** critical | Improve kitchen ventilation, move cooking outdoors |
| **NO2 (traffic pollution)** significant | Traffic regulation near residential areas |
| **Mother BMI** predictive | Nutrition programs for underweight mothers |
| **PM10** moderate impact | Air quality alerts during high pollution days |

### For Machine Learning

| Challenge | Lesson |
|-----------|--------|
| Class imbalance (mostly term births) | SMOTE helps but doesn't solve everything |
| High accuracy ≠ good model | MCC and AP reveal true performance |
| Transformer models need more data | TabNet/TabTransformer potential not fully realized |
| Feature engineering matters more than model | Environmental domain knowledge crucial |

---

## Limitations & Future Work

| Limitation | Proposed Solution |
|-----------|-------------------|
| Dataset limited to Dhaka region | Expand to other Bangladesh districts |
| Class imbalance persists | Explore advanced sampling, cost-sensitive learning |
| Cross-sectional data only | Longitudinal studies tracking pregnancy progression |
| Missing noise/soil/water pollution | Incorporate additional environmental sensors |
| No real-time prediction system | Deploy as web API for clinic use |

---

## Citation

If you use this work or the PreBEnvBD dataset, please cite:

```bibtex
@article{shuborna2026envirobirth,
  author    = {Tahsin Shuborna and Azizul Hakim and Namira Tasnim and Saha Reno},
  title     = {EnviroBirth: PreBEnvBD Dataset-Driven Prediction of Preterm Birth in Bangladesh Using Tree-Based and Deep Learning Models},
  journal   = {ICT Express},
  year      = {2026},
  publisher = {Elsevier}
}
```

**Dataset:** PreBEnvBD: Preterm Birth and Environmental Factors Dataset, Bangladesh
https://doi.org/10.5281/zenodo.19684670

---

## Contact

| Role | Contact |
|------|---------|
| **1st Author** | Tahsin Shuborna — shujaanat06@gmail.com |
| **2nd Author** | Azizul Hakim — azizulhakimshuvo185@gmail.com |
| **3rd Author** | Namira Tasnim — tas.nam.03@gmail.com |
| **Corresponding** | Saha Reno — reno.saha39@gmail.com |

**Interested in collaboration?** We're open to:
- Expanding PreBEnvBD to other Bangladesh regions
- Integrating additional environmental sensors
- Deploying real-time prediction systems
- Public health policy research partnerships

---

## License

This project is released under the **MIT License**.

The **PreBEnvBD dataset** is available on Zenodo under controlled access for research on preterm birth prediction in Bangladesh. Contact authors for access.

---

> *"Environmental pollution is a silent crisis for mothers and newborns. Data can help us act before it's too late."*
>
> — EnviroBirth Team, 2026

---

**Last Updated:** June 2026
**Status:** Manuscript Submitted to ICT Express

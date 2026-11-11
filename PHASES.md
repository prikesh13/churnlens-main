# ChurnLens — Development Phases Roadmap

This repository is built and released in **three progressive phases**, each representing a self-contained milestone.

---

## ✅ Phase 1 — Data Foundation & Core Segmentation
> **Branch / Tag:** `phase-1`

**What's included:**
- Project scaffolding (`README.md`, `requirements.txt`, `.gitignore`)
- Data ingestion with schema validation (`src/data/loader.py`)
- Full feature engineering pipeline (`src/data/preprocessor.py`)
- RFM scoring + K-Means segmentation (`src/features/segmentation.py`)
- Data download utility (`scripts/download_data.py`)
- Unit tests for the data layer (`tests/test_loader.py`, `tests/test_preprocessor.py`, `tests/test_segmentation.py`)

**Key outputs:**
- Clean, feature-engineered customer table ready for ML
- 4 named behavioural segments: Champions, Loyal Active, At-Risk, Hibernating

---

## ✅ Phase 2 — ML Models (Churn + CLV + Explainability)
> **Branch / Tag:** `phase-2`

**What's included:**
- Calibrated XGBoost churn classifier with SMOTE + Optuna HPO (`src/models/churn_model.py`)
- Discounted Cash Flow + BG/NBD CLV engine + retention priority matrix (`src/models/clv.py`)
- SHAP TreeExplainer for per-customer feature attribution (`src/models/shap_explainer.py`)
- Pre-trained model artifacts (`data/artifacts/xgb_model.pkl`, `shap_values.parquet`)
- Processed feature tables (`data/processed/`)
- Model-layer unit tests (`test_churn_model.py`, `test_clv.py`, `test_shap_explainer.py`)
- `evaluate_customer.py` — single-customer inference script

---

## ✅ Phase 3 — Streamlit Dashboard & Full Integration
> **Branch / Tag:** `phase-3`

**What's included:**
- 6-tab Streamlit dashboard (`dashboard/app.py`)
- Plotly chart library: gauge, waterfall, heatmap, radar (`dashboard/charts.py`)
- Cached artifact loader (`dashboard/loader.py`)
- Full end-to-end integration: raw CSV → dashboard in one command

---

## Running the Complete Project (All Phases)

```bash
# 1. Clone
git clone https://github.com/prikesh13/churnlens-main.git
cd churnlens-main

# 2. Create virtual environment
python3 -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Download raw data (optional if pre-computed artifacts are present)
python scripts/download_data.py

# 5. Run tests
pytest tests/ -v

# 6. Evaluate a customer
python evaluate_customer.py

# 7. Launch interactive dashboard
streamlit run dashboard/app.py
```

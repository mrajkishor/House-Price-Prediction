# House Price Prediction

End-to-end ML pipeline — data ingestion → feature engineering → model training → REST API serving.

## Project structure

```
House-Price-Prediction/
├── data/
│   ├── raw/          # original, immutable data drops
│   ├── processed/    # cleaned / feature-engineered datasets
│   └── external/     # third-party reference data
├── notebooks/        # exploratory analysis (EDA, prototyping)
├── src/              # production Python package
├── tests/            # pytest test suite
├── api/              # FastAPI inference service
├── docker/           # Dockerfiles and compose files
├── requirements.txt
└── README.md
```

## Quick start

```bash
# 1. Create and activate virtual environment
python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the API (once a model is trained)
uvicorn api.main:app --reload

# 4. Run tests
pytest --cov=src tests/
```

## Tech stack

| Layer | Tool |
|---|---|
| Data wrangling | pandas, numpy |
| ML models | scikit-learn, XGBoost, LightGBM |
| Experiment tracking | MLflow |
| API | FastAPI + Uvicorn |
| Testing | pytest |

## Status

Phase 1 — Project setup complete.

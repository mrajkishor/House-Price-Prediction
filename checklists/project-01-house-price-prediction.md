# Project 01 — House Price Prediction

**Difficulty:** ⭐☆☆☆☆ &nbsp;|&nbsp; **Use Case:** Proptech / Finance &nbsp;|&nbsp; **Tier:** Core Systems

**Concepts:** §1.2 · §1.3 · §2.1 · §2.2 · §2.3 · §3.1 · §3.2 · §3.4 · §3.5 · §8.3 · §8.4

---

## Phase 1 — Project Setup

- [ ] Create repo / folder structure (`data/`, `notebooks/`, `src/`, `tests/`, `api/`, `docker/`)
- [ ] Set up virtual environment (`venv` or `conda`)
- [ ] `requirements.txt` with pinned versions
- [ ] `.gitignore` — exclude data files, `.env`, `__pycache__`
- [ ] `README.md` stub — project description, how to run
- [ ] Initialise Git, first commit

---

## Phase 2 — Data

- [ ] Download Ames Housing dataset from Kaggle (`train.csv`, `test.csv`)
- [ ] Load into Pandas, inspect shape, dtypes, first/last rows
- [ ] Identify numerical vs categorical columns
- [ ] Check missing value counts (absolute + percentage per column)
- [ ] Check for duplicate rows

---

## Phase 3 — Exploratory Data Analysis (EDA)

- [ ] Plot target distribution (`SalePrice`) — check skewness
- [ ] Apply log transform to `SalePrice` if skewed, justify with statistics
- [ ] Correlation heatmap — top 15 features correlated with target
- [ ] Scatter plots: `GrLivArea`, `TotalBsmtSF`, `GarageArea` vs `SalePrice`
- [ ] Box plots for top categorical features (`Neighborhood`, `OverallQual`)
- [ ] Statistical test: t-test or ANOVA on key categorical groups (§1.3)
- [ ] Outlier analysis — visualise and document decision (keep / remove)
- [ ] Document 5+ key EDA findings in a markdown cell or section

---

## Phase 4 — Feature Engineering (§3.4)

- [ ] **Missing values**
  - [ ] Numerical: impute with median (or domain logic — e.g. `GarageYrBlt` → 0 if no garage)
  - [ ] Categorical: impute with mode or `"None"` where absence is meaningful
- [ ] **Encoding**
  - [ ] Ordinal encoding for ordered categories (`ExterQual`, `KitchenQual`, etc.)
  - [ ] One-hot encoding for nominal categories (low-cardinality)
  - [ ] Target encoding or frequency encoding for high-cardinality columns
- [ ] **Scaling** — StandardScaler or RobustScaler on numerical features
- [ ] **New features**
  - [ ] `TotalSF` = `TotalBsmtSF` + `1stFlrSF` + `2ndFlrSF`
  - [ ] `TotalBath` = full baths + 0.5 × half baths
  - [ ] `HouseAge` = `YrSold` − `YearBuilt`
  - [ ] `RemodAge` = `YrSold` − `YearRemodAdd`
  - [ ] At least 2 more engineered features of your own
- [ ] Save processed datasets (`train_processed.csv`, `test_processed.csv`)

---

## Phase 5 — Model Training (§3.1 · §3.2)

- [ ] Train/validation split — 80/20, stratified if applicable
- [ ] Define evaluation metrics: MAE, RMSE, R² (on log-transformed target)
- [ ] Build a **baseline** — mean prediction or simple Linear Regression
- [ ] Train **Linear Regression** — record metrics
- [ ] Train **Ridge Regression** — record metrics, note effect of L2 regularisation
- [ ] Train **Lasso Regression** — record metrics, note feature selection effect
- [ ] Train **Random Forest Regressor** — record metrics
- [ ] Train **XGBoost Regressor** — record metrics
- [ ] Compare all 5 models in a summary table (baseline vs each model)

---

## Phase 6 — Hyperparameter Tuning (§3.5)

- [ ] Install and import Optuna
- [ ] Write Optuna objective function for XGBoost (tune `n_estimators`, `max_depth`, `learning_rate`, `subsample`, `colsample_bytree`)
- [ ] Run study — minimum 50 trials
- [ ] Plot optimisation history and parameter importance
- [ ] Retrain best XGBoost with tuned params, record final metrics
- [ ] Compare pre-tuning vs post-tuning metrics explicitly

---

## Phase 7 — Model Explainability

- [ ] Install SHAP
- [ ] Compute SHAP values for best model on validation set
- [ ] Plot SHAP summary plot (beeswarm)
- [ ] Plot SHAP bar chart — top 15 most important features
- [ ] SHAP waterfall plot for 1 high-price and 1 low-price prediction
- [ ] Write 3–5 sentence interpretation: which features drive price most, and why it makes domain sense

---

## Phase 8 — Code Quality (§2.3)

- [ ] Refactor notebook logic into `src/` modules:
  - [ ] `src/data.py` — load, validate, split
  - [ ] `src/features.py` — all feature engineering functions
  - [ ] `src/train.py` — model training and evaluation
  - [ ] `src/predict.py` — load model, run inference
- [ ] All functions have docstrings
- [ ] `logging` set up — log key steps (data shape, metric scores, model saved)
- [ ] Write `tests/` with pytest:
  - [ ] Test feature engineering functions (null handling, expected output shapes)
  - [ ] Test model loads and prediction returns correct type/shape
- [ ] Run `pytest` — all tests passing

---

## Phase 9 — Model Serving (§8.3)

- [ ] Save final model with `joblib` or `pickle`
- [ ] Build `api/main.py` with FastAPI:
  - [ ] `GET /health` — returns `{"status": "ok"}`
  - [ ] `POST /predict` — accepts JSON with house features, returns predicted price
- [ ] Define Pydantic request/response schema
- [ ] Test endpoint locally with Swagger UI (`/docs`) or `curl`
- [ ] Handle edge cases — missing fields, invalid inputs → return useful error messages

---

## Phase 10 — Containerisation & Deployment (§8.4)

- [ ] Write `Dockerfile` — base image, install deps, copy src, expose port, `CMD`
- [ ] Build Docker image locally, test it works
- [ ] Write `docker-compose.yml` for local dev
- [ ] Deploy to Railway **or** Render (free tier)
- [ ] Confirm live endpoint returns predictions
- [ ] Note the public URL

---

## Phase 11 — Documentation & Presentation

- [ ] Update `README.md`:
  - [ ] Project description and use case
  - [ ] Architecture diagram (even a simple ASCII or draw.io export)
  - [ ] Before/after metrics table (baseline → best model → tuned model)
  - [ ] How to run locally
  - [ ] Live demo link
- [ ] Record a short demo video (Loom or screen record) — show the API returning a prediction
- [ ] Write a short write-up (300–500 words): decisions made, tradeoffs, what you'd do differently

---

## Completion Checklist

- [ ] All 5+ models trained and compared
- [ ] Hyperparameter tuning done with Optuna
- [ ] SHAP explainability plots generated
- [ ] `src/` modules written and tested
- [ ] FastAPI endpoint live and working
- [ ] Docker image builds successfully
- [ ] Deployed and publicly accessible
- [ ] README complete with metrics and demo link
- [ ] Demo video recorded

---

## Metrics to Beat

| Model | MAE | RMSE | R² |
|---|---|---|---|
| Baseline (mean) | — | — | ~0.00 |
| Linear Regression | — | — | — |
| Ridge | — | — | — |
| Lasso | — | — | — |
| Random Forest | — | — | — |
| XGBoost (untuned) | — | — | — |
| **XGBoost (tuned)** | — | — | **target: > 0.90** |

> Fill in your numbers as you train each model.

---

*Part of [AI/ML Engineering — 16 Systems](../projects.md)*

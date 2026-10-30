<div align="center">

<img src="assets/logo_lockup.png" alt="SkillMap" width="360">

### AI-Enabled Labour Market Intelligence & Skill Demand-Supply Forecasting Engine
**Smart India Hackathon 2026 | Problem Statement 26246 | Ministry of Skill Development and Entrepreneurship (MSDE)**

[![Python 3.9+](https://img.shields.io/badge/Python-3.9+-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.50+-FF4B4B?logo=streamlit&logoColor=white)](https://streamlit.io/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?logo=mysql&logoColor=white)](https://www.mysql.com/)
[![LightGBM](https://img.shields.io/badge/LightGBM-XGBoost-2F9E44)](https://lightgbm.readthedocs.io/)
[![SHAP](https://img.shields.io/badge/Explainability-SHAP-425B9A)](https://shap.readthedocs.io/)
[![Gemini](https://img.shields.io/badge/Gemini-optional-4285F4?logo=google&logoColor=white)](https://ai.google.dev/)
[![Languages](https://img.shields.io/badge/UI-7_Indian_languages-76C0EC)](#multi-language-and-voice)

*District-level skill forecasting | Shortage & oversupply risk detection | Seat-allocation recommendations | Data-grounded multilingual AI assistant*

</div>

---

## 📌 The Problem

India trains millions of youth every year across vocational and technical institutes. However, training seats are historically planned without dynamic, granular, district-level insights into employer demand. As a consequence:
- Fast-growing trades face acute worker shortages in emerging industrial hubs.
- Traditional trades continue over-enrolling trainees who struggle with unemployment.

**PS 26246 (MSDE)** mandates an intelligent Labour Market Information System (LMIS) engine that forecasts localized skill demand and supply, anticipates divergence, and produces actionable seat-reallocation guidance. **SkillMap** delivers this at 3, 6, and 12-month horizons with interpretable ML drivers and full transparency.

---

## 🏗️ System Architecture & Workflow

```
 Notebook (Feature Engineering, ML Models, SHAP, Back-testing)
        │
        ▼
 lmis_bundle.pkl  ──load_db.py──►  MySQL 8  ◄─── SQLAlchemy ───  FastAPI (api.py)
        │                                                              │
        │   (Fallback: App reads bundle directly;                      │  REST + Swagger Docs
        │    Assistant utilizes local SQLite copy)                     ▼
        └──────────────────────────────────────────────────►  Streamlit (app.py)
                                                                Dashboard │ Recommendation Engine │ Assistant
                                                                          │
                                                                Optional: Gemini rephrases SQL-grounded facts
```

### End-to-End Workflow

1. **Data Ingestion & Cleaning** — Ingests NCS-based demand records with automated auditing for missing periods, deduplication, standardized taxonomy, and outlier correction.
2. **Predictive Forecasting** — Benchmarks Linear Regression, LightGBM, XGBoost, Holt-Winters/ARIMA, and weighted ensembles. The best-performing model per horizon is picked based on rolling-origin splits.
3. **Gap & Risk Stratification** — Calculates localized gaps (`Forecast Demand - Forecast Supply`), mapping them to dynamic risk indices: *Low*, *Medium*, *High*, *Critical Shortage*, or *Oversupply*.
4. **Model Explainability** — SHAP values detail underlying drivers for rising or dropping demand; an auxiliary XGBoost classifier flags early-warning risk probabilities.
5. **Actionable Recommendations** — Translates risks into concrete seat actions: *Scale Capacity*, *Optimize Utilization*, *Downscale*, or *Reallocate* across neighbouring trades within the district.
6. **Ground-Truth Multilingual Assistant** — Answers natural queries by generating parametric SQL queries against verified data, optionally polished into human language via Gemini.

---

## 📸 Application Showcase

### Dashboard Overview
> Dynamic state, sector, and horizon filters with real-time KPI metrics, national summaries, and key vulnerability insights.

![Dashboard overview](screenshots/dashboard_overview.png)

---

### Geographic Heatmap & Drill-Down
> Interactive India tile map visualizing gap severity and high-risk clusters across states down to individual districts.

![Map and drill-down](screenshots/map_drilldown.png)

---

### Gap & Risk Analysis
> District-by-district demand vs. supply trajectories highlighting critical pressure points.

![Gap and risk](screenshots/gap_risk.png)

---

### Explainable AI (SHAP Drivers)
> Transparent feature attribution explaining why specific skills are projected to trend up or down.

![Explainability](screenshots/explainability.png)

---

### Model Accuracy & Validation
> Rigorous rolling-origin back-tests comparing ensemble and gradient boosted trees against naive baselines.

![Accuracy](screenshots/accuracy.png)

---

### Recommendation Engine & Action Plan
> Targeted seat adjustment policies ranked by urgency (P1 to P4) with target allocations.

![Recommendation action plan](screenshots/recommendation_action_plan.png)

---

### What-if Policy Simulator
> Stress-test seat modifications or demand shocks interactively before policy commitment.

![What-if simulator](screenshots/what_if.png)

---

### Multilingual Data-Grounded Assistant
> Ask complex queries in English or regional Indian languages with guaranteed numerical grounding.

![SkillMap Assistant](screenshots/assistant.png)

---

## ⚡ Feature Matrix

| Capability | Highlights |
|------------|------------|
| **Interactive Dashboard** | Macro national overview, geo-drilldown, historical curves, risk categorization, SHAP feature importance. |
| **Recommendation Engine** | Seat capacity optimization, same-district trade reallocation, budget constraints, policy simulator. |
| **Planner Target Exports** | Instant export of planned intake allocations into Excel (`.xlsx`), CSV, or printable brief PDFs. |
| **Data-Grounded Assistant** | Voice & text support, auto-generated data citations, SQL-backed persistence, Hinglish compatibility. |
| **Inclusive Design** | Dynamic text resizing, high-contrast mode, reduced motion, multilingual UI support. |
| **7 Indian Languages** | English, Hindi, Marathi, Tamil, Telugu, Bengali, Gujarati with embedded regional typography. |
| **High Performance** | SQLAlchemy connection pooling, query caching, gzip compression, fast SQLite local fallback. |

---

## 📊 Model Evaluation & Benchmarks

Back-tested across **9,072 rolling-origin forecasts** (63 districts × 12 skills across Apr 2022 – Mar 2026):

| Metric / Horizon | 3 Months | 6 Months | 12 Months |
|------------------|----------|----------|-----------|
| **Best Demand Model** | LightGBM | LightGBM | Ensemble (LightGBM + XGBoost) |
| **Demand WAPE (Test)** | ~7.3% | ~7.8% | ~8.5% |
| **Baseline WAPE (Naive)** | 11.2% | 13.4% | 15.1% |
| **Risk Classification Accuracy** | 61.4% (Macro F1: 0.59 vs Baseline: 0.56) |
| **Tolerance Rate (±1 Class)** | **> 91.0%** |

---

## 🚀 Quick Start Guide

### Prerequisites
- Python 3.9+ (Python 3.10 or 3.11 recommended)
- Optional: MySQL 8.0+ or Docker (for full client-server backend)

---

### Option A: Standalone Mode (Zero External Dependencies)
Runs completely standalone using bundled serialized artifacts (`lmis_bundle.pkl`) and automatic local SQLite generation:

```bash
# Clone the repository
git clone https://github.com/Manjeet077283/skill-map.git
cd skill-map

# Set up virtual environment
python -m venv venv
venv\Scripts\activate   # Windows
# source venv/bin/activate  # macOS / Linux

# Install dependencies
pip install -r requirements.txt

# Run Streamlit frontend
streamlit run app.py
```
*Access UI at:* `http://localhost:8501`

---

### Option B: Full-Stack Mode (MySQL + FastAPI + Streamlit)

```bash
# 1. Start MySQL 8 container
docker compose up -d

# 2. Configure environment credentials
cp .env.example .env
# Update .env if using custom MySQL / Gemini credentials

# 3. Initialize database & seed forecast tables
python load_db.py

# 4. Launch backend and frontend simultaneously
python run_all.py
```
*Or execute components independently:*
- **FastAPI Backend:** `uvicorn api:app --host 0.0.0.0 --port 8000` (Docs: `http://localhost:8000/docs`)
- **Streamlit Frontend:** `streamlit run app.py --server.port 8501`

*(On Windows, convenience runner `run.bat` is provided; on Unix use `./run.sh`)*

---

## ⚙️ Configuration (.env)

| Variable | Description | Default |
|----------|-------------|---------|
| `DATABASE_URL` | SQLAlchemy connection string | `mysql+pymysql://skillmap:skillmap_pw@localhost:3306/skillmap` |
| `API_URL` | Backend REST API URL for Streamlit client | `http://127.0.0.1:8000` |
| `GEMINI_API_KEY` | *(Optional)* Google Gemini API key for conversational phrasing | `""` *(Uses internal deterministic engine)* |
| `GEMINI_MODEL` | Gemini model variant | `gemini-2.0-flash` |
| `SKILLMAP_AUTOSTART` | Auto-launch local API if unreached | `0` |

---

## 🔌 API Reference

Full interactive Swagger OpenAPI documentation available at `http://localhost:8000/docs`.

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | `GET` | Service liveness & dependency health checks |
| `/areas` | `GET` | Catalog of available states, districts, and skill sectors |
| `/summary` | `GET` | Aggregated national-level demand, supply, and net gaps |
| `/forecast` | `GET` | 3/6/12-month predictions with confidence bounds for a district × skill |
| `/district/{district}` | `GET` | Comprehensive overview of all trades in a specific district |
| `/series` | `GET` | Filterable time-series records for analytical charting |
| `/high-risk` | `GET` | Critical shortage and severe oversupply priority lists |
| `/recommendations` | `GET` | Rule-based and model-guided seat allocation plans |
| `/whatif` | `POST` | Dynamic scenario simulations with seat and demand delta adjustments |
| `/explain` | `GET` | Local SHAP attribution scores & risk probabilities |
| `/targets` | `GET` | Automated policy intake figures (supports CSV / Excel / PDF) |
| `/chat` | `POST` | Natural language interface with verifiable SQL query grounding |

---

## 🗄️ Database Architecture

SkillMap features an optimized relational schema supporting high-throughput analytical queries:

- `dim_state`: State codes and administrative designations.
- `dim_district`: District entities cross-referenced with parent states.
- `dim_skill`: Standardized skill designations, NSQF classifications, and industry sectors.
- `fact_series`: Dimensional facts including baseline demand/supply, 3/6/12m forecasts, confidence intervals, gap indices, and risk classes.
- `fact_history`: Historical monthly panel data spanning 2022–2026.
- `kb_document`: Knowledge base chunks and policy references for Assistant context.
- `chat_log` & `chat_conversation`: Session histories and audit trails.

---

## 📂 Repository Structure

```
skill-map/
├── assets/                  # Logos, icons, branding assets
├── screenshots/             # Interface screenshots for documentation
├── notebook/                # Research notebooks & feature engineering pipelines
│   └── LMIS_Part1_Part2.ipynb
├── .streamlit/              # Streamlit theme and UI configurations
├── api.py                   # FastAPI REST API service & database queries
├── app.py                   # Streamlit multi-page interface & assistant bridge
├── load_db.py               # Database migration and ingestion script
├── local_db.py              # Zero-config SQLite generator for standalone use
├── run_all.py               # Multi-process orchestrator for API + UI
├── schema.sql               # MySQL / MariaDB relational DDL schema
├── docker-compose.yml       # Containerized MySQL service definition
├── requirements.txt         # Pinned Python package dependencies
├── .env.example             # Safe template for environment configuration
├── LICENSE                  # MIT Open Source License
└── README.md                # Comprehensive project documentation
```

---

## 🛡️ Data Transparency & Disclaimers

1. **Demand Data** — Derived and normalized from official National Career Service (NCS) vacancy postings.
2. **Supply Simulation** — In the absence of an open real-time central trainee registry, supply figures are statistically modeled and anchored to verified district-level PMKVY FY2021–22 throughput. The ingestion interface is built to seamlessly bind to live training registries when available.
3. **Multilingual Transliteration** — Translations are verified programmatically; feedback from native linguists is encouraged.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!
1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for more information.

---

<div align="center">

**SkillMap — The Right Skills, in the Right District, at the Right Time.**

*Smart India Hackathon 2026 | PS 26246 | Ministry of Skill Development and Entrepreneurship*

Developed with ❤️ by **Manjeet Yadav** & the SkillMap Team.

</div>

# 💹 FINSIGHT — Financial Intelligence System
### Automated Annual Report Intelligence Pipeline | RINL (Vizag Steel) FY 2024-25

[![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)](https://www.python.org/)
[![SQLite](https://img.shields.io/badge/Database-SQLite-lightgrey?logo=sqlite)](https://www.sqlite.org/)
[![Power BI](https://img.shields.io/badge/Dashboard-Power%20BI-F2C811?logo=powerbi)](https://powerbi.microsoft.com/)
[![NLP](https://img.shields.io/badge/NLP-TextBlob-green)](https://textblob.readthedocs.io/)
[![License](https://img.shields.io/badge/License-Confidential-red)](#)

---

## 📌 Overview

**FINSIGHT** is an end-to-end financial intelligence system built on the **43rd Annual Report (FY 2024-25)** of **Rashtriya Ispat Nigam Limited (RINL)**, India's principal government-owned steel manufacturer.

The system automates the complete analytical pipeline — from raw PDF ingestion to an interactive executive dashboard — transforming what traditionally requires weeks of manual analyst effort into a **replicable, one-hour deployment**.

> 📄 Source Document: RINL 43rd Annual Report 2024-25 | 380 pages | 8.7 MB PDF

---

## 🔑 Key Results

| Metric | Finding |
|--------|---------|
| 📉 Revenue FY25 | ₹18,288 Crores (−21% YoY — market-driven, not operational) |
| 📉 Debt Reduction | ₹18,616 Cr → ₹11,672 Cr (**−37% in a single year**) |
| 📈 Loss Improvement | ₹4,849 Cr → ₹1,389 Cr (**−71% net loss**) |
| 🏥 Financial Health Score | **22.3 / 100** (stressed, recovering) |
| ⚠️ Highest Risk | Regulatory Risk — 51 mentions in MDA text |
| 🔮 Bull Case FY28 | ₹29,779 Crores revenue, positive PAT by FY26-27 |

---

## 🏗️ Architecture

```
📄 RINL Annual Report PDF (380 pages, 8.7 MB)
        │
        ▼
┌─────────────────────┐
│   ETL Pipeline      │  pdfplumber → pandas → SQLAlchemy
│   5 tables extracted│  clean_number(), bracket-to-negative conversion
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│   SQLite Database   │  11 domain-specific tables
└────────┬────────────┘
         │
    ┌────┴─────────────────────────────────┐
    │                                      │
    ▼                                      ▼
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  Financial   │  │  NLP Risk    │  │  Scenario    │
│  Scorecard   │  │  Engine      │  │  Forecasting │
│  21 Ratios   │  │  290 paras   │  │  Bull/Base/  │
│  /100 score  │  │  TextBlob    │  │  Bear FY28   │
└──────┬───────┘  └──────┬───────┘  └──────┬───────┘
       │                 │                  │
       └────────┬────────┘                  │
                │                           │
                ▼                           ▼
        ┌───────────────────────────────────────┐
        │     Power BI Executive Dashboard      │
        │         7-page interactive report     │
        └───────────────────────────────────────┘
```

---

## 🧩 Modules

### 1. ETL Pipeline
- Extracts **5 key financial tables** across 6 pages using `pdfplumber`
- Custom `clean_number()` function handles Indian bracket-notation negatives (e.g., `(1,388.62)` → `-1388.62`)
- Loads cleaned data into **11-table SQLite database**

### 2. Financial Scorecard
- Computes **21 financial ratios** across 4 dimensions: Profitability, Liquidity, Leverage, Efficiency
- Benchmarks against **Damodaran 2024 Metals & Mining sector norms**
- Weighted composite scoring → **Financial Health Score: 22.3/100**

| Dimension | Weight | RINL Score |
|-----------|--------|------------|
| Profitability | 35% | 6.5/100 |
| Liquidity | 25% | 2.0/100 ⚠️ |
| Leverage | 20% | 3.0/100 |
| Efficiency | 20% | 6.0/100 |
| **Composite** | **100%** | **22.3/100** |

### 3. Segment Analysis (BCG Matrix)
| Segment | Revenue Share | YoY Growth | BCG Quadrant |
|---------|--------------|------------|--------------|
| Structural Steel | 35% | +11.5% | ⭐ STAR |
| Wire Rods | 28% | +8.2% | ⭐ STAR |
| Rounds & Blooms | 18% | −5.0% | 🐕 DOG |
| Pig Iron | 10% | −12.0% | 🐕 DOG — Exit |
| By-Products | 9% | +15.0% | ❓ QUESTION MARK |

### 4. NLP Risk Engine
- Classifies **290 MDA paragraphs** into 6 risk categories using domain-specific keyword dictionaries
- Severity formula: `Severity = (Keyword Score × 0.4) + (Negativity × 4) + (Severity Word Count × 0.3)`

| Risk Category | Paragraphs | Avg Severity | Signal |
|---------------|-----------|-------------|--------|
| Regulatory | 51 | 0.55 | 🔴 Highest Frequency |
| Market | 28 | 0.59 | 🟡 Medium |
| Technology | 23 | 0.48 | 🟢 Low |
| Operational | 19 | 0.65 | 🔴 Highest Severity |
| Financial | 14 | 0.46 | 🟡 Low freq, High impact |
| Geopolitical | 2 | 0.40 | 🟢 Rare |

### 5. Three-Scenario Forecast (FY25-26 to FY27-28)
| Scenario | FY 2025-26 | FY 2026-27 | FY 2027-28 | PAT Outlook |
|----------|-----------|-----------|-----------|------------|
| 🟢 Bull Case | ₹21,946 Cr | ₹25,895 Cr | ₹29,779 Cr | Positive PAT by FY26-27 |
| 🟡 Base Case | ₹20,483 Cr | ₹22,531 Cr | ₹24,333 Cr | Positive PAT by FY27-28 |
| 🔴 Bear Case | ₹17,374 Cr | ₹17,895 Cr | ₹18,790 Cr | Losses through FY28 |

### 6. Power BI Dashboard
- 7-page interactive executive dashboard covering all analytical modules
- Includes Revenue Trend, Debt Reduction, BCG Matrix, Risk Heatmap, Forecast Scenarios, Sensitivity Analysis, and Radar Chart

---

## 🛠️ Tech Stack

| Layer | Tools |
|-------|-------|
| PDF Extraction | `pdfplumber` |
| Data Processing | `pandas`, `numpy` |
| Database | `SQLite 3.x`, `SQLAlchemy` |
| NLP | `TextBlob` |
| Visualization | `matplotlib`, Power BI Desktop |
| Execution | Google Colab (cloud) |
| Language | Python 3.12 |

---

## 📂 Project Structure

```
FINSIGHT/
├── config.yaml                  # Single config file — update to deploy on any company
├── etl/
│   ├── extract.py               # pdfplumber table extraction
│   ├── clean.py                 # clean_number(), data standardization
│   └── load.py                  # SQLAlchemy → SQLite loader
├── scorecard/
│   ├── ratios.py                # 21 financial ratio calculations
│   ├── scoring.py               # Damodaran benchmark scoring
│   └── radar_chart.png          # Output visualization
├── segments/
│   ├── bcg_matrix.py            # BCG quadrant classification
│   └── bcg_chart.png
├── risk/
│   ├── nlp_engine.py            # Keyword classification + TextBlob sentiment
│   ├── risk_register.csv        # 290-paragraph risk output
│   └── risk_heatmap.png
├── forecasting/
│   ├── scenarios.py             # Bull/Base/Bear scenario modeling
│   ├── sensitivity.py           # Sensitivity analysis matrix
│   └── forecast_chart.png
├── data/
│   ├── rinl_financial.db        # 11-table SQLite database
│   └── clean_historical.csv     # 5-year historical baseline
└── dashboard/
    └── RINL_Dashboard.pbix      # Power BI executive dashboard
```

---

## 🚀 Deployment

This pipeline is **fully reusable**. To run it on any company's annual report:

1. Clone this repository
2. Place the target annual report PDF in `/data/`
3. Update `config.yaml` with the PDF path and relevant page numbers
4. Run the pipeline end-to-end

```bash
# Install dependencies
pip install pdfplumber pandas numpy textblob sqlalchemy matplotlib

# Run ETL
python etl/extract.py

# Run all analytical modules
python scorecard/ratios.py
python segments/bcg_matrix.py
python risk/nlp_engine.py
python forecasting/scenarios.py
```

> ⏱️ Full pipeline execution: ~1 hour on any company's annual report

---

## 📊 Key Findings Summary

1. **Revenue decline is structural, not operational** — RINL maintained production volumes; price realizations fell due to Chinese steel dumping
2. **Debt restructuring is the biggest value driver** — ₹6,944 Cr net debt reduction saves ~₹625 Cr in annual interest at current rates
3. **Raw material concentration is the core vulnerability** — Coal & Iron Ore = 52% of total costs (₹12,179 Cr); a 10% price drop saves ~₹823 Cr
4. **Structural Steel + Wire Rods = franchise products** — 63% of revenue, both growing
5. **Pig Iron is destroying value** — 12% decline, strategic exit recommended
6. **FY 2025-26 is the make-or-break year** — Management guidance projects positive PAT; Bull Case confirms it is achievable

---

## 🏢 Project Context

| Field | Details |
|-------|---------|
| Organization | Rashtriya Ispat Nigam Limited (RINL / Vizag Steel Plant) |
| Department | IT & ERP, CSM — Visakhapatnam Steel Plant |
| Project Guide | KNSS Yadav, DGM (IT & ERP) |
| Analyst | Faustena S., M.Sc. Data Science, CHRIST (Deemed to be University), Bengaluru |
| Academic Institution | CHRIST (Deemed to be University), Bengaluru — Batch 2025-27 |
| Document | RINL 43rd Annual Report 2024-25 |
| Classification | CONFIDENTIAL — for academic and management review |

---

## ⚠️ Limitations

- Covers RINL **standalone** financials only (no consolidated/subsidiary data)
- Forecast uses structured scenario analysis — no ML-based forecasting models
- PDF extraction accuracy is dependent on `pdfplumber`; merged cells required manual verification
- Quarterly or intra-year data is out of scope

---

## 👩‍💻 Author

**Faustena S.**  
M.Sc. Data Science | CHRIST (Deemed to be University), Bengaluru  
[GitHub](https://github.com/Faustena25) · [LinkedIn](#)

---

*This project is confidential and intended for academic review and RINL management use only. All financial data is sourced directly from RINL's 43rd Annual Report 2024-25.*

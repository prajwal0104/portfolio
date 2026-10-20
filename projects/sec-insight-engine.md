# SEC Insight Engine: 10-K/10-Q Balance Sheet & Ratio Auditor

[![Python](https://img.shields.io/badge/Python-3.11%2B-blue.svg)](https://www.python.org/)
[![SEC EDGAR](https://img.shields.io/badge/Data-SEC%20EDGAR%20API-informational.svg)](https://www.sec.gov/edgar)
[![Pydantic](https://img.shields.io/badge/Validation-Pydantic%20v2-e92063.svg)](https://pydantic.dev/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Privacy](https://img.shields.io/badge/Repository-Private-critical.svg)](#)

An autonomous financial filing ingestion and balance sheet analysis engine that parses SEC EDGAR HTML/XBRL filings, normalizes GAAP accounting items, computes core solvency and liquidity ratios, and grades corporate balance sheet health.

Built on **BeautifulSoup4**, **Playwright**, **Pydantic v2**, and **Rich**.

---

## 🎯 Architecture & Data Flow

```mermaid
flowchart TD
    Ticker[Company Ticker / CIK] --> EDGARFetcher[SEC EDGAR Ingestion Pipeline]
    EDGARFetcher --> HTMLParser[10-K / 10-Q HTML & XBRL Parser]
    HTMLParser --> BalanceSheetExtractor[Consolidated Balance Sheet Extractor]
    BalanceSheetExtractor --> Normalizer[GAAP Line-Item Normalizer]
    Normalizer --> RatioCalculator[Financial Ratio Computation Engine]
    RatioCalculator --> Solvency[Solvency & Liquidity: Current, Quick, D/E]
    RatioCalculator --> Profitability[Profitability & Efficiency: ROE, ROA]
    Solvency & Profitability --> HealthGrader[Balance Sheet Health Scoring]
    HealthGrader --> Report[Financial Dossier & Audit Table]
```

---

## 🔬 Working Model & CLI Execution Walkthrough

### Example Command
```bash
python -m src.main --ticker AAPL --filing-type 10-K
```

### Live Working Model Output
```text
╭──────────────────────────────────────────────────────────────────────────────╮
│                       📊 SEC Insight Engine v1.0.0                           │
│   Auditing Filing: AAPL | Form: 10-K (Annual Report) | GAAP Normalized       │
╰──────────────────────────────────────────────────────────────────────────────╯

Consolidated Balance Sheet Summary ($ Millions):
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┓
┃ Line Item                              ┃ FY 2025          ┃ FY 2024          ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━┫
┃ Cash and Cash Equivalents              ┃ $  29,943        ┃ $  28,840        ┃
┃ Total Current Assets                   ┃ $ 143,713        ┃ $ 135,405        ┃
┃ Total Current Liabilities              ┃ $ 145,308        ┃ $ 125,481        ┃
┃ Total Long-Term Debt                   ┃ $  95,281        ┃ $  98,959        ┃
┃ Total Shareholders' Equity             ┃ $  62,146        ┃ $  60,275        ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━━━┛

Financial Health & Ratio Analysis:
┏━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┓
┃ Financial Ratio     ┃ Calculated Value ┃ Industry Median  ┃ Health Rating    ┃
┣━━━━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━┫
┃ Current Ratio       ┃ 0.99             ┃ 1.20             ┃ Fair / Stable    ┃
┃ Quick Ratio         ┃ 0.84             ┃ 0.95             ┃ Moderate         ┃
┃ Debt-to-Equity      ┃ 1.53             ┃ 1.80             ┃ Healthy          ┃
┃ Working Capital     ┃ - $ 1,595 M      ┃ + $ 4,200 M      ┃ High Cash Flow Req┃
┗━━━━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━━━┛

Balance Sheet Health Grade: A- (Exceptional operational cash flow offsets negative working capital)
```

---

## ⚡ Core Features

- **SEC Submissions API Integration**: Complies with SEC fair-access rate limits with structured User-Agent declarations.
- **Robust GAAP Tag Resolution**: Normalizes disparate terminology across US-GAAP reporting entities (e.g. `MarketableSecurities` vs `ShortTermInvestments`).
- **Audit Anomaly Detection**: Flags aggressive restatements, unusual debt expansions, and goodwill write-downs.

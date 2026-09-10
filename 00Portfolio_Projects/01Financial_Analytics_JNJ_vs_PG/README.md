# Comparative Financial Analytics: Johnson & Johnson vs. Procter & Gamble

## Overview

This project is a comparative financial and strategic analysis of
**Johnson & Johnson (J&J)** and **The Procter & Gamble Company (P&G)**
over fiscal years **2019--2021**.

Originally developed from an MBA Financial Accounting group project,
this version was substantially reconstructed and extended as an
independent **financial analytics portfolio project**. The objective is
to demonstrate how accounting data, corporate filings, and business
information can be transformed into structured, decision-relevant
insights using financial analysis and data analytics methods.

Rather than asking which company is simply "better," the project
examines how differences in **profitability, liquidity, operating
efficiency, financial risk, product mix, geographic growth, and
corporate transactions** reveal two distinct financial and strategic
profiles.

> **Portfolio purpose:** This repository demonstrates my
> interdisciplinary preparation in financial analysis, business
> analytics, data interpretation, and research-oriented problem solving
> as part of my PhD applications in Business Analytics and related
> fields.

## Research Question

**How do differences in profitability, liquidity, operating efficiency,
financial risk, product mix, geographic growth, and portfolio
transactions reveal the contrasting financial and strategic profiles of
Johnson & Johnson and Procter & Gamble during 2019--2021?**

## Analytical Framework

The project integrates seven complementary areas:

1.  **Profitability and Earnings Quality** --- gross, operating, and net
    margins; ROE; earnings measures; and unusual items.
2.  **Liquidity** --- current, quick, and cash ratios.
3.  **Operating and Working-Capital Efficiency** --- receivables,
    inventory, payables, operating cycle, cash conversion cycle, and
    asset turnover.
4.  **Solvency and Financial Risk** --- debt-to-assets, debt-to-equity,
    and interest coverage.
5.  **Product and Segment Analytics** --- segment trends, growth
    decomposition, and portfolio structure.
6.  **Geographic Expansion** --- U.S. versus international sales,
    regional growth, and segment-by-geography analysis.
7.  **Acquisitions and Divestitures** --- major transactions and
    portfolio reconfiguration.

## Data Sources

The analysis prioritizes **primary corporate disclosures** and materials
from the original project.

### Primary Sources

-   Johnson & Johnson annual reports / Form 10-K filings
-   Procter & Gamble annual reports / Form 10-K filings
-   Company financial statements, segment disclosures, geographic
    disclosures, and related notes

### Project Data

-   Original MGT 211 final project report
-   Supporting financial-ratio tables
-   Original geographic-expansion Excel workbook
-   Reconstructed tables from the original report where raw spreadsheets
    were no longer available

Where possible, reconstructed figures were cross-checked against company
filings. The portfolio also corrects analytical interpretations from the
original coursework when they conflict with the underlying data or
standard financial logic.

## Methods

The project combines **cross-sectional** and **time-series** financial
analysis. Methods include financial ratio analysis, trend analysis,
cross-company benchmarking, growth-rate analysis, CAGR, segment and
geographic decomposition, working-capital cycle analysis, data
reconstruction and validation, comparative visualization, and strategic
interpretation.

An important part of the workflow is moving beyond mechanical ratio
calculation. Financial metrics are interpreted in the context of each
company's **business model, segment structure, fiscal calendar, unusual
accounting items, and strategic activities**.

## Selected Findings

### J&J: Financial Strength and International Pharmaceutical Growth

J&J displayed higher gross margins, stronger conventional liquidity,
lower balance-sheet leverage, substantially higher interest coverage,
and strong Pharmaceutical growth. Pharmaceutical sales increased from
approximately **\$42.2 billion in 2019 to \$52.1 billion in 2021**.
International sales also grew faster than U.S. sales over the study
horizon.

### P&G: Working-Capital Efficiency and Consumer-Category Resilience

P&G's most distinctive characteristic was its working-capital
efficiency. The company maintained a **negative cash conversion cycle**
throughout the study period, indicating that cash was generally
collected from customers before corresponding supplier payments were
made.

Growth was particularly notable in **Fabric & Home Care** and **Health
Care**, while U.S. sales grew faster than international sales during the
analyzed period.

### Why Context Matters

P&G's fiscal 2019 reported profitability was materially affected by a
large non-cash goodwill and intangible-asset impairment charge. A purely
mechanical comparison would therefore misinterpret the persistence of
the company's underlying operating performance.

> **Financial analytics should explain the economic mechanisms behind
> reported numbers, not simply rank companies by ratios.**

## Data Quality and Analytical Corrections

Reconstructing the original project also provided an opportunity to
audit its methodology.

For example, the original report stated that J&J had a *lower* interest
coverage ratio and connected this to stronger solvency. The underlying
data showed the opposite: **J&J's interest coverage was substantially
higher than P&G's**. Because higher interest coverage generally
indicates greater earnings capacity relative to interest expense, the
portfolio version corrects this interpretation.

Similarly, a calculation originally labeled an "average growth rate" was
actually cumulative percentage growth from 2019 to 2021. The revised
analysis distinguishes cumulative growth from CAGR.

These corrections are documented rather than silently changing the
historical project.

## Key Takeaway

The analysis does not identify a universal financial "winner." Instead,
it reveals two different financial systems.

**Johnson & Johnson:** higher structural margins, stronger conventional
liquidity, lower leverage, greater debt-service coverage,
pharmaceutical-led growth, and stronger international expansion.

**Procter & Gamble:** exceptional working-capital efficiency, a negative
cash conversion cycle, resilient consumer-staples operations, strong
Fabric & Home Care and Health Care growth, and faster U.S. growth during
the study period.

The broader lesson is that **profitability, liquidity, efficiency,
solvency, product mix, geography, and strategy must be analyzed
jointly**. A single financial ratio rarely provides enough information
to explain firm performance.

## Suggested Repository Structure

``` text
financial-analytics-jnj-pg/
├── README.md
├── report/
│   └── Financial_Analytics_Portfolio_JNJ_vs_PG.pdf
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
│   └── financial_analysis.ipynb
├── src/
│   └── analysis.py
├── figures/
│   ├── profitability.png
│   ├── liquidity.png
│   ├── cash_conversion_cycle.png
│   ├── interest_coverage.png
│   ├── segment_growth.png
│   └── geographic_growth.png
└── references/
    └── source_notes.md
```

> The repository can be expanded toward this fully reproducible
> structure as the analytical workflow is migrated from the original
> spreadsheet/PDF materials into code.

## Limitations

-   J&J and P&G use different fiscal year-end dates, so fiscal-year
    labels do not represent identical calendar periods.
-   The companies operate in different industries, meaning some ratio
    differences reflect business-model economics rather than managerial
    performance alone.
-   Parts of the original group project were available only as PDF
    tables rather than raw spreadsheets.
-   The 2019--2021 period includes the COVID-19 shock.
-   The study is descriptive and comparative rather than causal.
-   Market-based valuation and shareholder-return analysis are outside
    the current scope.

## Project Provenance

This project originated as a collaborative final project for an MBA
Financial Accounting course, with tasks divided among group members.

My original responsibility focused on the **World Expansion / Geographic
Expansion** analysis, for which the underlying Excel workbook was
retained.

For this portfolio version, the complete project was reconstructed and
extended into an integrated financial analytics study. All major
sections are treated with equal analytical importance, including
sections originally prepared by other group members. Where original
spreadsheets were unavailable, historical tables were reconstructed from
the final report and validated against primary company disclosures where
possible.

This provenance is disclosed to maintain transparency regarding the
relationship between the original collaborative coursework and the
present portfolio project.

## Future Extensions

Potential extensions include rebuilding the dataset from SEC XBRL
filings, creating a reproducible Python pipeline, extending the time
horizon, adding peer firms and panel data, incorporating valuation and
shareholder-return measures, testing relationships between segment mix
and performance, studying post-acquisition outcomes, developing
interactive dashboards, and applying statistical or econometric models.

## Author

**Keman Xiang**

MBA graduate with interests in **Business Analytics, Financial
Analytics, Data Analytics, and empirical business research**.

This project is part of my research and analytical portfolio for PhD
applications.

## Disclaimer

This project is intended for **academic and portfolio purposes only**.
It does not constitute investment advice. Financial information is based
on historical company disclosures and project materials, and analytical
conclusions should be interpreted within the stated scope and
limitations.

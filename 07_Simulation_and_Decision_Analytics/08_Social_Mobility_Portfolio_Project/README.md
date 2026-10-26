# Intergenerational Social Mobility: A Markov Chain Simulation

**MGT239 — Simulation for Business | Research Portfolio Project**  
**Author:** Keman Xiang

## Project Overview

This project investigates **how socioeconomic status evolves across generations** using a **three-state, discrete-time Markov chain** and **Monte Carlo simulation in Microsoft Excel**. The model tracks family lines among **upper, middle, and lower** social levels, examining **whether initial status matters in the long run**, **how rapidly differences between family origins fade**, and **whether upward and downward mobility require comparable waiting times**.

The analysis distinguishes **aggregate convergence** from **individual mobility opportunities**: a stable long-run social distribution can coexist with asymmetric barriers to movement between social levels.

## Research Questions

|Question|Analytical focus|
|---|---|
|Q1 — Long-run distribution|Do three distinct initial social distributions approach similar class shares after 50 generations?|
|Q2 — Mobility trajectories|How does the probability of occupying the upper level evolve for Adam (initially upper) and Cooper (initially lower) over generations 1–10?|
|Q3 — First-passage times|How many generations does it take, on average, for Adam's descendants to first reach the lower level and Cooper's to first reach the upper level?|
|Q4 — Implications|What do convergence, persistence, and directional asymmetry suggest for decision analysis and social-policy discussion?|

## Model and Simulation Design

Social status is represented by three discrete states:

|State|Social level|Illustrative occupational categories|
|---|---|---|
|1|Upper|Executive, managerial, high-administrative, professional|
|2|Middle|High-grade supervisory, non-manual, skilled manual|
|3|Lower|Semi-skilled, unskilled|

The one-generation transition matrix is:

|Current state → Next state|Upper (1)|Middle (2)|Lower (3)|
|---|---|---|---|
|Upper (1)|0.45|0.48|0.07|
|Middle (2)|0.05|0.70|0.25|
|Lower (3)|0.01|0.50|0.49|

For a distribution vector **fₜ**, the population evolves according to **fₜ₊₁ = fₜP**. The simulation implements each transition using cumulative probabilities and Excel's `RAND()`, `INDEX()`, and `MATCH()` functions.

|Design element|Specification|
|---|---|
|Simulation horizon|50 generations|
|Sample size|1,000 simulated family lines|
|Initial distributions for long-run comparison|[0.5, 0, 0.5]; [1, 0, 0]; [0, 0, 1]|
|Adam|Starts in Upper (state 1)|
|Cooper|Starts in Lower (state 3)|
|Mobility-path output|P(Upper) for generations 1–10|
|First-passage output|Mean generations and 95% confidence interval|
|Simulation environment|Microsoft Excel; formula-driven stochastic paths|

## Results

The figures below describe **one saved Monte Carlo realization** documented in the accompanying research report. Because the Excel model uses `RAND()`, results can vary slightly after recalculation.

### 1. Long-run social distribution

|Initial distribution|Upper|Middle|Lower|
|---|---|---|---|
|[0.5, 0, 0.5]|6.0%|64.0%|30.0%|
|[1, 0, 0]|6.7%|62.9%|30.4%|
|[0, 0, 1]|5.5%|62.7%|31.8%|

By generation 50, the three simulations produce similar class distributions despite their sharply different starting conditions. The **middle level accounts for approximately 62.7%–64.0%** of family lines, while the largest across-scenario difference in any one class share is **1.8 percentage points**. This is consistent with convergence toward the stationary distribution implied by the transition matrix.

### 2. Adam versus Cooper: probability of reaching the upper level

|Generation|Adam P(Upper)|Cooper P(Upper)|Absolute difference|
|---|---|---|---|
|1|47.3%|1.0%|46.3 percentage points|
|2|See report / workbook|See report / workbook|18.4 percentage points|
|3|See report / workbook|See report / workbook|8.0 percentage points|
|5|See report / workbook|See report / workbook|1.2 percentage points|
|10|6.5%|7.7%|1.2 percentage points|

The strong generation-1 advantage associated with Adam's upper-level starting position diminishes rapidly. By generation 10, the simulated upper-level probabilities are close, and small differences between the curves should be interpreted in light of Monte Carlo sampling variation. The accompanying report and workbook contain the full ten-generation trajectories and charts.

### 3. First-passage time

|Mobility direction|Mean generations|95% confidence interval|
|---|---|---|
|Upper → Lower (Adam)|5.47|5.22–5.72|
|Lower → Upper (Cooper)|23.55|22.52–24.58|

The estimated lower-to-upper first-passage time is approximately **4.3 times** the upper-to-lower time. This asymmetry is consistent with the model's one-generation transition probabilities: **1%** for a direct lower-to-upper move versus **7%** for a direct upper-to-lower move. In the simulation engine, paths that do not reach their target within 50 generations are coded as 51; the reported statistics retain that finite-horizon convention.

## Interpretation and Implications

The results illustrate an important distinction: **long-run convergence of population shares does not imply symmetric mobility for individual families**. A system may approach a stable aggregate composition while still presenting different expected waiting times for movement between desirable and undesirable states.

This transition-based framework can also inform business analysis involving customer segments, employee levels, credit-risk categories, supplier quality, or other discrete states. For social policy, education, taxation, and welfare can be considered as potential mechanisms that might alter transition probabilities; however, **the present model does not estimate causal effects of any intervention**.

## Limitations

- Transition probabilities are fixed over time and identical for families occupying the same state.
- The first-order Markov assumption excludes earlier family history and unobserved heterogeneity.
- Three social categories simplify a much richer socioeconomic structure.
- Estimates vary across Monte Carlo realizations because `RAND()` recalculates.
- First-passage calculations use a finite 50-generation horizon, with no-hit paths coded as 51.
- Findings are **model-based simulation results**, not empirical causal estimates of real-world mobility or policy effectiveness.

## Project Files

|File|Description|
|---|---|
|`MGT239_Social_Mobility_Portfolio.xlsx`|Final Excel workbook containing the project overview, linked results dashboard, original simulation engine, charts, and documentation.|
|`Social_Mobility_Markov_Chain_Simulation_Report.pdf`|Research-style report presenting the background, Markov framework, methodology, simulation findings, interpretation, implications, and limitations.|
|`README.md`|GitHub entry point summarizing the research questions, model, results, and deliverables.|

## Reproducibility

Open the Excel workbook in Microsoft Excel and inspect `00_Project_Overview`, `01_Results_Dashboard`, `2Social_Mobility`, and `03_Documentation`. The original simulation formulas and named ranges are preserved in `2Social_Mobility`. Pressing **F9** recalculates random draws and updates the linked dashboard; the research report documents a specific saved realization rather than promising identical numbers after recalculation.

## Methods Demonstrated

**Markov-chain modeling · Monte Carlo simulation · Excel-based stochastic modeling · Transition-matrix analysis · Convergence interpretation · First-passage analysis · Confidence intervals · Data visualization · Decision-oriented interpretation**

---

*Keman Xiang PhD Application Portfolio*

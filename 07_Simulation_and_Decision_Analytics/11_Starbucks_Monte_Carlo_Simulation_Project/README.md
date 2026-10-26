# Starbucks Store Profitability: A Three-Scenario Monte Carlo Simulation

**Business Analytics · Monte Carlo Simulation · Spreadsheet Modeling · Decision Analysis**

This project examines how uncertainty in **supply-chain costs, inflation, customer demand, and mobile-app adoption** can affect the monthly profitability of a **hypothetical Starbucks store**. Using three separate Monte Carlo models implemented in Excel, the analysis traces uncertain inputs through operational assumptions, pricing rules, demand responses, revenue, and profit.

The purpose is **scenario-based decision analysis**, not a prediction of Starbucks' actual store-level financial performance. Model parameters are illustrative; public Starbucks disclosures provide business context rather than the numerical inputs.

## Research Questions

1. **Supply-chain disruption:** What happens to profit when procurement cost increases, the selling price rises, and customer demand is uncertain?
2. **Inflation and price elasticity:** How does inflation affect profit when both prices and procurement costs rise, while demand responds to price changes?
3. **Mobile-app adoption:** Can app-enabled staffing savings improve profit when a lower labor cost is fully passed through to the selling price?

## Project Files

|File|Description|
|---|---|
|`Starbucks_Monte_Carlo_Simulation.xlsx`|Final spreadsheet model, simulation results, convergence diagnostics, and methodology documentation.|
|`Starbucks_Monte_Carlo_Simulation_Research_Report.pdf`|Research-style report explaining the business problem, assumptions, models, saved results, interpretation, and limitations.|
|`README.md`|Project overview and navigation.|

## Analytical Workflow

**Problem → Model → Simulation Design → Results → Interpretation → Managerial Implications → Limitations**

1. Define a simplified monthly store baseline and separate scenario-specific cost assumptions.
2. Specify uncertain inputs using Normal, Uniform, and Beta distributions.
3. Apply the relevant pricing, demand, and operating-cost equations.
4. Generate **1,000 Monte Carlo observations per core scenario**.
5. Summarize profit, baseline-relative changes, outcome distributions, and Monte Carlo mean uncertainty.
6. Examine running means and, for Simulation 3, independent replication batches.
7. Interpret implications subject to the assumptions and exclusions of each model.

## Model Specifications

|Feature|Simulation 1: Supply Shock|Simulation 2: Inflation|Simulation 3: App Adoption|
|---|---|---|---|
|Primary uncertainty|Demand: Normal(8,000, 1,000²)|Inflation: Uniform(2%, 5%)|App adoption: Beta(5, 3); labor cost conditional on adoption|
|Baseline price|$4.00|$4.00|$4.00|
|Baseline quantity|10,000 purchased cups|10,000 purchased cups|10,000 cups of demand|
|Modeled cost|Full purchased-inventory cost|Full purchased-inventory cost|Monthly labor cost only|
|Baseline modeled profit|$15,000/month|$15,000/month|$37,000/month|
|Demand mechanism|Independently imposed stochastic demand|Linear signed elasticity, −1.2|Linear signed elasticity, −1.2|
|Sales cap|10,000 cups|10,000 cups|No cap; demand assumed fulfilled|

### Simulation 1 — Supply-Chain Shock

The model raises the procurement cost per cup from **$2.50 to $3.00** and the selling price from **$4.00 to $4.80**, while independently drawing monthly demand from a Normal distribution with mean **8,000** and standard deviation **1,000** cups. Sales are limited to the 10,000 purchased cups. All purchased inventory is expensed in the modeled month, even if some remains unsold.

**Profit = $4.80 × min(demand, 10,000) − $30,000.**

The demand reduction is an **assumption**, not an estimated causal effect of the price increase.

### Simulation 2 — Inflation and Price Elasticity

A uniformly distributed inflation rate between **2% and 5%** affects both selling price and procurement cost, in addition to the 20% supply-chain shock. Customer demand responds to the **signed price change** using a linear price-elasticity approximation with **Ed = −1.2**.

- **Price:** `4 × 1.2 × (1 + inflation rate)`
- **Demand:** `INT(10,000 × [1 − 1.2 × (price − 4) / 4])`
- **Profit:** `price × min(demand, 10,000) − 10,000 × 2.5 × 1.2 × (1 + inflation rate)`

Inflation is the random driver; demand is deterministic conditional on the inflation draw.

### Simulation 3 — Mobile-App Adoption and Labor Cost

App adoption follows **Beta(5, 3)**. If adoption is **50% or less**, monthly labor cost stays at **$3,000**. If adoption exceeds 50%, labor cost is drawn from **Normal(2,000, 500²)** and **clipped to the interval [$0, $3,000]**. Clipping is not the same as redrawing from a truncated Normal distribution.

The model assumes full proportional pass-through of labor savings into the coffee price:

- **Price:** `4 × labor cost / 3,000`
- **Demand:** `MAX(0, INT(10,000 × [1 − 1.2 × (price − 4) / 4]))`
- **Revenue:** `price × demand`
- **Profit:** `revenue − labor cost`

Unlike Simulations 1 and 2, **10,000 cups is a demand baseline, not a sales cap**, and supply-chain costs and inflation are excluded. App adoption affects profit **through the staffing threshold**, not as a direct multiplier of revenue.

## Results: Saved Workbook Snapshot

The following figures are taken from the **saved calculation snapshot** documented in the research report, using 1,000 draws per scenario. Since the spreadsheet uses volatile `RAND()` formulas, recalculation can produce different numerical results.

|Scenario|Mean Monthly Profit|Change vs. Own Baseline|P(Profit Below Baseline)|95% Simulation Outcome Interval|
|---|---:|---:|---:|---|
|1 · Supply-chain shock|$8,356.03|−44.3%|91.3%|−$410.52 to $17,228.16|
|2 · Inflation and elasticity|$4,225.71|−71.8%|100.0%|$3,213.54 to $5,149.25|
|3 · Mobile-app adoption|$34,753.67|−6.1%|55.9%|$24,844.70 to $37,621.38|

**Important:** Simulations 1 and 2 use a **$15,000 procurement-cost baseline**; Simulation 3 uses a **$37,000 labor-only baseline**. Their absolute profit levels are **not directly comparable as like-for-like operating outcomes**.

For Simulation 3, the saved draws show **62.3% mean app adoption**, **77.2%** above the staffing threshold, **$2,233.02 average labor cost**, **$2.98 average selling price**, and **13,067.5 average monthly cups demanded**. Although the labor bill falls on average, full pass-through into lower prices can reduce revenue enough to lower profit.

## Simulation Diagnostics and Visualizations

The workbook includes scenario output summaries, original model charts, and a **convergence** worksheet showing how cumulative mean profit changes as more draws are included. Under independent draws with finite variance, Monte Carlo standard error typically decreases approximately in proportion to **1/√n**.

The analysis distinguishes:

|Diagnostic|Interpretation|
|---|---|
|95% confidence interval for the simulated mean|Precision of the estimated mean under the assumed model; calculated approximately as `mean ± 1.96 × sample SD / √n`.|
|95% simulation outcome interval|2.5th–97.5th percentile range of **individual** simulated monthly outcomes.|
|Running mean / convergence|Checks numerical stability as the number of simulation draws grows; does **not** establish real-world model validity.|
|Simulation 3 replication batches|12 independent sets of 1,000 draws, implemented with ordinary spreadsheet formulas for Excel/WPS compatibility; these are **not 12 months**.|

The research report contains additional figures showing the app-adoption mechanism, simulated profit distributions, baseline-relative results, and cumulative mean profit.

## Managerial and Analytical Implications

- **Price increases do not guarantee higher profit.** Fixed procurement commitments and weak demand can overwhelm higher unit prices.
- **Cost shocks and customer responses must be modeled together.** Inflation-driven price changes affect both unit economics and demand.
- **Digital adoption is not equivalent to profit improvement.** A staffing threshold can reduce labor cost, but full price pass-through may erode revenue.
- **Sensitivity analysis is essential.** Real decisions should test alternative elasticity estimates, inventory policies, staffing thresholds, partial price pass-through, and operating constraints.

## Limitations

This is an **illustrative, hypothetical store model**, not an empirical causal study. Distribution parameters, demand elasticity, the app adoption threshold, and pricing rules are assumed rather than estimated from Starbucks transaction or payroll data. The model omits various real-world costs and constraints, including corporate overhead, taxes, app implementation and maintenance, capacity, service quality, and some inventory effects. Simulation 1 treats purchased inventory as an immediate modeled-period expense; Simulation 3 assumes all demand can be fulfilled. The linear elasticity approximation and the proportional cost-to-price rule are simplifications.

The results therefore describe **conditional implications of the specified assumptions**, not forecasts of actual Starbucks profitability.

## Reproducibility

1. Open `Starbucks_Monte_Carlo_Simulation.xlsx` in Excel or WPS.
2. Read the project guide and methods documentation, then inspect the core calculation sheet and scenario results.
3. Recalculate the workbook to generate new Monte Carlo draws; results will vary because of `RAND()`.
4. Use the live-results and convergence worksheets to inspect changes in estimates and simulation stability.
5. For an exact reproduction of the **reported saved snapshot**, preserve the original cached outputs or export the draw-level values before recalculation.

## References

1. Starbucks Corporation. (2022). [Form 10-K for fiscal year ended October 2, 2022](https://www.sec.gov/Archives/edgar/data/829224/000082922422000058/sbux-20221002.htm).
2. Starbucks Corporation. (2022, September 13). [Starbucks enters new era of growth driven by an unparalleled Reinvention Plan](https://investor.starbucks.com/news/financial-releases/news-details/2022/Starbucks-Enters-New-Era-of-Growth-Driven-by-an-Unparalleled-Reinvention-Plan/default.aspx).
3. Starbucks Corporation. (2022). [Fiscal 2022 Annual Report](https://investor.starbucks.com/files/doc_financials/2022/ar/Starbucks-FY22-Annual-Report.pdf).

---

**Keman Xiang PhD Application Portfolio**

# Auction Mechanisms and Optimal Bidding Strategies

### A Monte Carlo Simulation Study of Bidder Surplus and Seller Revenue

**Author:** Keman Xiang  
**Project area:** Simulation for Business · Auction Theory · Decision Analytics  
**Methods:** Monte Carlo simulation, independent private values, equilibrium bidding, revenue equivalence, convergence diagnostics  
**Tools:** Microsoft Excel / WPS-compatible formulas and charts

## Project Overview

How should a seller select an auction mechanism, and how aggressively should a bidder bid when competitors' valuations are unknown?

This project examines a stylized land sale in which **CA**, the owner of a single parcel, considers **two sealed-bid auction mechanisms:** **first-price** (the winner pays their own bid) and **second-price** (the winner pays the second-highest bid). The analysis distinguishes two objectives that are easy to conflate: maximizing **bidder surplus** and maximizing **seller revenue**.

A fixed-sample Monte Carlo model evaluates bidder behavior and auction outcomes under different competitive conditions. The accompanying research report develops the economic rationale, documents the model, interprets the numerical findings, and discusses their implications for auction design and decision-making.

> **Scope:** This is a model-based computational study, not an empirical analysis of observed real-estate transactions. All monetary outcomes are in **millions of US dollars ($M)**.

## Research Questions

1. **Bidding incentives:** Which fraction of private valuation should bidder 1 submit to maximize expected surplus in each auction format?
2. **Seller proceeds:** How does bidder 1's bidding strategy affect the seller's expected revenue?
3. **Competition:** How do outcomes change as the number of bidders increases from 2 to 5 to 10?
4. **Mechanism comparison:** Do first-price and second-price auctions generate similar expected seller revenue when bidders use their benchmark equilibrium strategies?
5. **Simulation precision:** How stable are the Monte Carlo estimates as the number of replications grows?

## Model and Auction Rules

Each of the **N** risk-neutral bidders observes their own private valuation, independently drawn from **Uniform(0, 1)**. Bidder 1 submits a bid equal to **x × valuation**, where **x** ranges from 0.1 to 1.0 in increments of 0.1. Rival bidders follow the mechanism-specific benchmark strategy.

|Feature|First-price sealed-bid auction|Second-price sealed-bid auction|
|---|---|---|
|Allocation|Highest bid wins|Highest bid wins|
|Winner's payment|Their own bid|Second-highest bid|
|Bidder 1 strategy|`b1 = x × v1`|`b1 = x × v1`|
|Rival strategy|`bi = ((N − 1)/N) × vi`|`bi = vi`|
|Bidder 1 surplus if winning|`v1 − b1`|`v1 − highest rival bid`|
|Seller revenue|Highest bid|Second-highest bid|
|Theoretical bidder 1 optimum|`x* = (N − 1)/N`|`x* = 1` (truthful bidding)|

The equilibrium seller-revenue benchmark under these assumptions is **E[R] = (N − 1)/(N + 1)**. Revenue equivalence applies to *expected revenue at equilibrium*, not to individual auction realizations or arbitrary deviations from equilibrium bidding.

## Simulation Design

|Design element|Implementation|
|---|---|
|Auction mechanisms|First-price; second-price|
|Number of bidders|`N = 2, 5, 10`|
|Bidder 1 bid coefficients|`x = 0.1, 0.2, ..., 1.0`|
|Monte Carlo replications|1,000 for each bidder-count scenario|
|Valuation distribution|Independent `Uniform(0, 1)`|
|Outputs|Bidder 1 surplus and seller revenue|
|Simulation matrices|12 matrices: 2 mechanisms × 3 bidder counts × 2 outcomes|
|Matrix dimensions|1,000 replications × 10 strategies|
|Variance-control design|Fixed common valuation draws across strategies and mechanisms for each `N`|
|Reproducibility|Random valuations are stored as fixed values in the workbook|

**Workflow:** Generate and retain private valuations → apply the auction-specific bidding rule → identify the winner and payment → calculate bidder surplus and seller revenue → repeat over strategies and replications → compute expected outcomes → compare equilibrium results with theory → examine convergence and Monte Carlo uncertainty.

## Main Results

### Optimal Bidder Strategies and Surplus

|Number of bidders|First-price optimal x|First-price surplus ($M)|Second-price optimal x|Second-price surplus ($M)|
|---|---|---|---|---|
|2|0.5|0.164415|1.0|0.164690|
|5|0.8|0.033928|1.0|0.033918|
|10|0.9|0.010406|1.0|0.010577|

**Interpretation:** In a first-price auction, bidding more aggressively increases the chance of winning but reduces surplus when the bidder wins; the best balance changes with competition. In a second-price auction, truthful bidding is weakly dominant under the stated assumptions. As the number of competitors increases, bidder 1's optimal expected surplus decreases sharply.

### Seller Revenue and Revenue Equivalence

The table compares seller revenue **at each mechanism's equilibrium strategy**; it does not compare maximum seller revenue across off-equilibrium bid coefficients.

|Number of bidders|Theoretical revenue ($M)|First-price revenue ($M)|Second-price revenue ($M)|Second − First ($M)|
|---|---|---|---|---|
|2|0.333333|0.334320|0.339390|+0.005070|
|5|0.666667|0.662739|0.667931|+0.005192|
|10|0.818182|0.818503|0.817852|−0.000650|

**Interpretation:** Expected seller revenue increases with bidder participation. Both auction mechanisms produce estimates close to the theoretical revenue benchmark, while the small observed differences vary in sign. These finite-sample differences do not establish that one mechanism systematically earns more in equilibrium.

### Convergence and Uncertainty

The workbook's convergence analysis tracks cumulative average seller revenue as simulation replications increase. Early averages fluctuate more; estimates become more stable with additional replications and approach the model's theoretical benchmarks. The report also provides Monte Carlo standard errors and approximate 95% Monte Carlo intervals for equilibrium seller revenue. These quantify **simulation error under the model**, not uncertainty about actual land-market prices.

## Figures and Visual Analysis

The companion report contains four figures derived from the fixed-sample workbook:

|Figure|What it shows|Analytical purpose|
|---|---|---|
|1. Expected bidder surplus|Surplus by bid coefficient and auction mechanism|Locate optimal bidder strategies and illustrate bid shading|
|2. Expected seller revenue|Revenue by bid coefficient for `N = 2, 5, 10`|Separate seller incentives from bidder incentives|
|3. Equilibrium revenue comparison|First-price, second-price, and theoretical revenue|Evaluate revenue equivalence across bidder counts|
|4. Monte Carlo convergence|Running mean revenue and theoretical benchmark|Assess stabilization of simulation estimates|

The Excel workbook also includes the original twelve mechanism-specific charts and additional strategy and convergence visualizations.

## Managerial and Analytical Implications

**For the seller (CA):** Under this benchmark model, first-price and second-price auctions yield similar expected proceeds at equilibrium. Mechanism choice should therefore not be justified by isolated simulated price differences alone. Practical considerations outside this model—including bidder familiarity, administration, participation, and institutional rules—may matter.

**For bidders:** The payment rule determines the bidding incentive. First-price bidders benefit from equilibrium bid shading, whereas truthful bidding is weakly dominant in the second-price setting with independent private values.

**For analysts:** A transparent simulation should separate objectives, hold uncertain inputs comparable across policy alternatives, report simulation precision, and distinguish theoretical equilibrium claims from finite-sample numerical findings.

## Workbook Guide

|Worksheet|Purpose|
|---|---|
|`00_READ_ME`|Project background, research questions, and navigation|
|`01_RESEARCH_MODEL`|Economic assumptions, bidding rules, and payoff definitions|
|`02_SIMULATION_DESIGN`|Experimental factors, random inputs, and reproducibility|
|`03_RESULTS_DASHBOARD`|Optimal strategies and equilibrium outcome summaries|
|`04_STRATEGY_CURVES`|Strategy-by-strategy surplus and revenue profiles|
|`05_CONVERGENCE`|Running means and Monte Carlo uncertainty diagnostics|
|`06_INTERPRETATION`|Economic interpretation of simulated outcomes|
|`07_IMPLICATIONS_LIMITS`|Managerial implications, limitations, and extensions|
|`08_CALCULATION_GUIDE`|Explanations of sample paths, data tables, STAT, and questions|
|`1_First_Price`|First-price sample-path calculations, simulation matrices, summaries, and charts|
|`2_Second_Price`|Second-price calculations, summaries, charts, and mechanism comparison|
|`MC_Random_N2`|Fixed valuation draws for two bidders|
|`MC_Random_N5`|Fixed valuation draws for five bidders|
|`MC_Random_N10`|Fixed valuation draws for ten bidders|

### Understanding the Calculation Sheets

- **Sample Path:** A worked auction realization showing how private valuations translate into bids, allocation, payments, bidder surplus, and seller revenue.
- **Data Tables:** Ten strategy columns evaluated across 1,000 simulated valuation vectors. Separate tables store bidder surplus and seller revenue for each bidder count.
- **STAT / Summary:** Column means estimate expected surplus or expected revenue at a specified strategy; these are averages of simulated outcomes, not additional random draws.
- **Questions and interpretation:** Explain the optimization of bidder surplus, how strategies affect seller revenue, the effect of bidder participation, and comparisons across auction mechanisms.

## Files

|File|Description|
|---|---|
|`Auction_Mechanisms_Research_Portfolio.xlsx`|Primary research workbook with model calculations, fixed simulations, summaries, charts, and documentation|
|`Auction_Mechanisms_Research_Report.pdf`|Full research-style report, including theoretical framework, results, figures, discussion, limitations, and references|
|`README.md`|Project overview, methodology, key results, workbook navigation, and interpretation|

## Reproducibility Notes

1. Open the Excel workbook and start with `00_READ_ME`, followed by `01_RESEARCH_MODEL` and `02_SIMULATION_DESIGN`.
2. Review `03_RESULTS_DASHBOARD`, `04_STRATEGY_CURVES`, and `05_CONVERGENCE` for the reported estimates and figures.
3. Trace any result to the corresponding mechanism-specific calculation sheet and its fixed valuation worksheet.
4. **Do not replace the fixed valuation cells with `RAND()`** if you want to reproduce the published numerical results exactly.
5. Monetary values are in millions of dollars; displayed numbers may be rounded. The simulation matrices and their formulas are the numerical source of record.

## Limitations and Future Research

The model assumes risk neutrality, independent uniformly distributed private valuations, symmetric knowledge of the valuation distribution, one indivisible asset, and fixed rival strategies. It does not model correlated/common values, asymmetric bidders, reserve prices, collusion, financing constraints, entry decisions, or endogenous participation. The bid grid is discrete and each bidder-count configuration uses 1,000 replications. Possible extensions include finer strategy grids, alternative valuation distributions, reserve-price optimization, bidder heterogeneity, more replications, and paired inference for mechanism differences.

## References

- Vickrey, W. (1961). *Counterspeculation, auctions, and competitive sealed tenders*. The Journal of Finance, 16(1), 8–37. https://doi.org/10.1111/j.1540-6261.1961.tb02789.x
- Morris, T. P., White, I. R., & Crowther, M. J. (2019). *Using simulation studies to evaluate statistical methods*. Statistics in Medicine, 38(11), 2074–2102. https://doi.org/10.1002/sim.8086

---

*Keman Xiang PhD Application Portfolio*

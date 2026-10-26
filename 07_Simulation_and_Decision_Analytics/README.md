# Simulation & Decision Analytics

**11 Excel-Based Projects | Simulation for Business**  
**Keman Xiang**

## Overview

This collection brings together 11 projects developed in *MGT239: Simulation for Business*. The projects use Excel-based simulation and quantitative modeling to examine uncertain outcomes, dynamic processes, and decisions in marketing, operations, finance, healthcare, and economics.

The emphasis is on **how a model works, what its simulated outcomes mean, and how those outcomes can inform decisions**. The portfolio progresses from sampling and Monte Carlo methods to stochastic price processes, Markov chains, diffusion models, and an integrated Starbucks profitability simulation.

> **Reproducibility note:** Many workbooks contain volatile functions such as `RAND()`. Recalculation can generate a different simulation run. Numerical findings cited below reflect documented runs and should not be treated as invariant model outputs.

## Project Index

| No. | Project | Main Methods | Application |
|---|---|---|---|
| 01 | [Monte Carlo Simulation & Statistical Estimation](#01-monte-carlo-simulation--statistical-estimation) | Random sampling, confidence intervals, convergence | Estimation under uncertainty |
| 02 | [Sales Promotion & Flextrola](#02-sales-promotion--flextrola) | Monte Carlo simulation, profit modeling, scenarios | Sales and operational decisions |
| 03 | [Asian Option Pricing & Hedging](#03-asian-option-pricing--hedging) | Simulated price paths, payoff modeling | Derivatives and financial risk |
| 04 | [Investment Strategies & Insurance](#04-investment-strategies--insurance) | Scenario simulation, return and loss distributions | Financial decision-making |
| 05 | [Market Share Dynamics](#05-market-share-dynamics--markov-chains) | Markov chains, customer-level simulation | Brand switching and competition |
| 06 | [Bass Diffusion Model](#06-bass-diffusion-model--product-adoption) | Innovation–imitation diffusion, dynamic forecasting | New-product adoption |
| 07 | [Healthcare Infectious Disease Simulation](#07-healthcare-infectious-disease-simulation) | Stochastic dynamic simulation, intervention comparison | Health and economic outcomes |
| 08 | [Social Mobility Across Generations](#08-social-mobility-across-generations) | Markov chains, transition matrices | Intergenerational mobility |
| 09 | [First-Price & Second-Price Auctions](#09-first-price--second-price-auctions) | Auction simulation, bidding and payment rules | Competitive bidding |
| 10 | [Credit Rating Simulation](#10-credit-rating-simulation) | Stochastic credit-state modeling | Credit risk |
| 11 | [Starbucks Business Simulation](#11-starbucks--integrated-business-simulation) | Monte Carlo simulation, price–demand–cost scenarios | Pricing and profitability |

---

## 01. Monte Carlo Simulation & Statistical Estimation

**Business/analytical question:** How reliably can a quantity be estimated from simulated random samples, and how does precision change with sample size?

**Approach and methods:**
- Generate random observations and compute sample statistics in Excel.
- Compare sample means and confidence intervals across sample sizes of **100, 500, 1,000, and 5,000**.
- Examine sampling variability, interval width, and convergence as the number of observations increases.

**Interpretation:** A single simulation run is not a certainty. Larger samples generally produce more stable estimates and narrower confidence intervals, providing a practical foundation for reporting uncertainty in subsequent projects.

**Skills:** Random sampling · Monte Carlo methods · Sample statistics · Confidence intervals · Convergence

## 02. Sales Promotion & Flextrola

**Business/analytical question:** How do uncertain demand and operating conditions affect the profitability of business decisions?

**Approach and methods:**
- **Sales Promotion:** Simulate uncertain demand and prices, realized sales, leftover inventory, discount revenue, procurement costs, stockouts, and total profit.
- Compare financial outcomes across repeated random trials rather than relying on a single demand forecast.
- **Flextrola:** Apply a separate spreadsheet-based business simulation to evaluate outcomes under uncertain assumptions and decision scenarios.

**Interpretation:** Revenue and profit do not necessarily move together. Inventory constraints, purchasing costs, and the treatment of unsold goods can change which decision performs best. The precise Flextrola model specifications should be read alongside its original workbook.

**Skills:** Monte Carlo simulation · Inventory economics · Profit modeling · Scenario comparison

## 03. Asian Option Pricing & Hedging

**Business/analytical question:** How can financial instruments whose payoffs depend on uncertain price paths be valued and assessed for risk?

**Approach and methods:**
- Simulate possible paths of an underlying asset price.
- Compute the average price over an observation window and use it to determine an Asian option payoff.
- Aggregate simulated payoffs to examine estimated option values and variability.
- Explore the financial implications of hedging positions under different simulated paths.

**Interpretation:** Path-dependent instruments cannot be understood from a single terminal-price scenario. Simulation exposes both estimated value and the range of possible payoffs. Specific pricing assumptions and hedge definitions are retained in the workbook.

**Skills:** Stochastic price paths · Asian options · Payoff simulation · Financial risk

## 04. Investment Strategies & Insurance

**Business/analytical question:** How should alternative financial choices be compared when returns and losses are uncertain?

**Approach and methods:**
- Simulate outcomes for two investment strategies and compare their return distributions.
- Examine downside exposure alongside expected performance.
- Use an insurance simulation to assess uncertain losses and the financial consequences of protection decisions.

**Interpretation:** A higher expected return need not imply a preferable risk profile. Simulation makes potential adverse outcomes visible and supports comparisons that go beyond averages. Detailed assumptions and any numerical conclusions depend on the saved workbook runs.

**Skills:** Investment simulation · Risk–return analysis · Insurance modeling · Decision-making under uncertainty

## 05. Market Share Dynamics — Markov Chains

**Business/analytical question:** How do customer retention and brand-switching probabilities shape competitive market shares over time?

**Approach and methods:**
- Define a **transition probability matrix** describing customers remaining with or switching between competing brands.
- Use a **macro-level model** to propagate aggregate market shares through successive periods.
- Use a **micro-level model** to simulate individual customer transitions and aggregate them into market shares.
- Compare simulated trajectories with analytical long-run or steady-state behavior.
- Explore how changes in switching probabilities, including promotional interventions, can affect outcomes.

**Interpretation:** Long-run market share depends on transition behavior, not merely initial market share. Comparing individual-based simulation with aggregate analysis helps explain how customer-level dynamics produce market-level results.

**Skills:** Markov chains · Transition matrices · Customer switching · Micro/macro modeling · Steady states

## 06. Bass Diffusion Model — Product Adoption

**Business/analytical question:** How might adoption of a new product evolve from launch through growth and eventual market saturation?

**Approach and methods:**
- Apply the **Bass Diffusion Model** to a hypothetical product, **Q-Phone**.
- Distinguish adoption associated with **innovation** (external influence) from adoption associated with **imitation** (influence from existing adopters).
- Model period-by-period new adopters, cumulative adoption, and the remaining potential market.
- Examine the shape and timing of the product-adoption lifecycle.

**Interpretation:** New-period sales can peak and then decline even as cumulative adoption continues to rise. Diffusion modeling helps distinguish a maturing addressable market from an isolated short-term sales change.

**Skills:** Bass diffusion · Dynamic forecasting · Innovation and imitation · Product lifecycle analysis

## 07. Healthcare Infectious Disease Simulation

**Business/analytical question:** How does a protective intervention alter disease trajectories, population outcomes, and an associated economic measure in a stylized population?

**Approach and methods:**
- Track susceptible individuals, infected individuals, and cumulative deaths in a stochastic dynamic model.
- Simulate **100 periods** and **1,000 villages per scenario**.
- Compare a baseline **without protection** against a scenario **with protection**.
- Estimate outcome probabilities, cumulative economic results, and confidence intervals; assess simulation convergence.

**Selected documented results:**

| Outcome | Without Protection | With Protection |
|---|---:|---:|
| Probability of complete population die-out | 99.3% | 56.0% |
| Average cumulative tax revenue per village | $12.610 million | $17.141 million |

The modeled protection scenario reduced the probability of complete population die-out by **43.3 percentage points** and increased average cumulative tax revenue by approximately **$4.531 million per village** in the documented runs.

**Interpretation:** Interventions can change both population survival and economic outcomes within a dynamic system. These figures arise from a hypothetical simulation; they are **not real-world epidemiological forecasts or causal estimates**.

**Skills:** Stochastic systems · Intervention analysis · Monte Carlo replication · Probability estimation · Confidence intervals

## 08. Social Mobility Across Generations

**Business/analytical question:** How do intergenerational transition probabilities affect social-class persistence and long-run mobility?

**Approach and methods:**
- Represent social position using three states: **upper**, **middle**, and **lower**.
- Define a transition matrix for movements between classes across generations.
- Simulate **1,000 family trajectories** using Excel random-number and lookup functions, including `RAND()`, `MATCH()`, and `INDEX()`.
- Compare outcomes from different initial distributions and examine behavior through **50 generations**.

**Selected documented result:** By generation 50, the simulated distributions under different initial conditions became similar. The upper-class share was approximately **5.5%–6.7%**, and the middle-class share approximately **62.7%–64.0%** across the reported scenarios.

**Interpretation:** Initial conditions can matter substantially in the short run, while long-run proportions can converge under a fixed transition system. The result is conditional on the model's transition probabilities, not an empirical claim about actual societies.

**Skills:** Markov chains · Intergenerational transitions · Long-run convergence · Individual trajectory simulation

## 09. First-Price & Second-Price Auctions

**Business/analytical question:** How do auction payment rules affect bidder incentives and the distribution of seller revenue?

**Approach and methods:**
- Simulate bidder valuations and bids in sealed-bid auctions.
- **First-price auction:** The highest bidder wins and pays their own winning bid.
- **Second-price auction:** The highest bidder wins and pays the second-highest bid.
- Compare winning payments, bidder outcomes, and simulated auction revenue under the modeled assumptions.

**Interpretation:** Mechanism design changes incentives, not only the final payment calculation. Comparisons must account for bidding assumptions; revenue equivalence or strategic optimality should not be inferred from an isolated simulation without supporting assumptions.

**Skills:** Auction simulation · Bidding rules · Mechanism comparison · Revenue analysis

## 10. Credit Rating Simulation

**Business/analytical question:** How can changes in credit quality over time be represented and assessed probabilistically?

**Approach and methods:**
- Represent credit quality using discrete rating states.
- Model uncertain future rating outcomes and, where specified in the workbook, transitions between rating categories.
- Summarize the distribution of possible credit states and consider implications for risk assessment.

**Interpretation:** Credit quality is not necessarily static. A stochastic framework helps evaluate uncertainty in future states instead of relying on a single fixed rating. The workbook is the authoritative source for its exact rating categories, transition assumptions, and computed results.

**Skills:** Credit-state modeling · Stochastic risk · Probability-based financial analysis

## 11. Starbucks — Integrated Business Simulation

**Business/analytical question:** Can higher prices offset inflation and operating-cost pressures without eroding demand and overall profitability?

**Approach and methods:**
- Build an integrated model linking **prices, demand, revenue, operating costs, and profit**.
- Represent uncertainty through Monte Carlo simulation and evaluate outcomes over a **12-month** horizon.
- Conduct **1,000 simulation trials** in the documented project.
- Examine pricing and demand sensitivity, inflation and cost assumptions, and scenarios involving mobile-app usage and labor costs.
- Compare expected financial outcomes and the distribution of simulated profit under alternative scenarios.

**Main interpretation:** Under the project's assumptions, price increases can reduce overall profit when demand is sufficiently price-sensitive. The analysis motivates considering operational efficiency and cost-management strategies alongside price adjustments.

This is a **course-based decision-support model**, not a validated forecast of Starbucks' actual future financial performance.

**Skills:** Integrated Monte Carlo modeling · Pricing analytics · Demand elasticity · Cost scenarios · Profitability analysis

---

## Shared Analytical Workflow

| Stage | Purpose | Typical Excel Implementation |
|---|---|---|
| 1. Problem definition | Identify the decision, uncertain inputs, and outcomes | Assumptions and input cells |
| 2. Model construction | Express relationships between inputs and outputs | Formulas, probability distributions, transition matrices |
| 3. Simulation | Generate possible realizations | `RAND()`, conditional logic, repeated trials |
| 4. Output analysis | Summarize variability and estimation uncertainty | Means, distributions, probabilities, confidence intervals |
| 5. Scenario comparison | Evaluate interventions or alternative choices | Side-by-side models, sensitivity tables, charts |
| 6. Interpretation | Translate modeled outcomes into qualified insights | Project reports and written discussion |

## Methods and Application Areas

| Method | Projects | Decision-Analytics Relevance |
|---|---|---|
| Monte Carlo simulation | 01, 02, 03, 04, 07, 09, 11 | Quantifies uncertainty in possible outcomes |
| Markov and state-transition modeling | 05, 08; credit-state concepts in 10 | Describes evolving systems and long-run distributions |
| Dynamic adoption modeling | 06 | Connects product diffusion to lifecycle planning |
| Financial risk simulation | 03, 04, 10 | Examines uncertain payoffs, returns, and credit outcomes |
| Marketing and operations simulation | 02, 05, 06, 11 | Connects demand and behavior to managerial choices |
| Intervention and scenario analysis | 02, 05, 07, 11 | Compares modeled alternatives under stated assumptions |

## Files and Reproducibility

Each project folder can contain the original Excel workbook, a project-specific README, a report where available, and supporting figures. The workbooks are the computational source of truth; reports provide context, interpretation, and limitations.

To review a project:
1. Read its description and assumptions.
2. Open the corresponding `.xlsx` workbook in Microsoft Excel.
3. Inspect inputs, formulas, simulation outputs, and charts.
4. If recalculating, expect results to change when random-number formulas are present.
5. Use the report's documented run when comparing exact numerical findings.

## Scope and Limitations

These are graduate coursework models and portfolio analyses. Some scenarios are hypothetical or intentionally simplified to isolate a modeling concept. Their results should be interpreted **conditional on the stated assumptions**; they are not automatically causal findings, empirical forecasts, or externally validated policy recommendations.

For projects whose detailed workbook assumptions are not reproduced in this overview, consult the original spreadsheet before citing specific distributions, parameters, or numerical outcomes.

## Author

**Keman Xiang**  
  
**Keman Xiang PhD Application Portfolio**

**Interests:** Business Analytics · Data Science · Quantitative Modeling · Decision-Making Under Uncertainty

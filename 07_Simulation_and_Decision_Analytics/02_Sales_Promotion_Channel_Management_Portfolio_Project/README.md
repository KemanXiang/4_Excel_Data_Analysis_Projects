# Sales Promotion & Channel Management under Uncertainty

## Monte Carlo Simulation \| Inventory Optimization \| Decision Analysis \| Excel

This project develops two spreadsheet-based Monte Carlo simulation
models to analyze **inventory decisions under uncertainty**. The
analysis examines how pre-season order quantities affect expected
profit, stockout risk, service performance, and excess inventory when
firms must make decisions before uncertain demand and market outcomes
are realized.

The project contains two related applications:

1.  **Sales Promotion Inventory Planning** --- determining an
    appropriate inventory level for a furniture promotion under
    uncertain demand and selling price.
2.  **Flextrola Channel Management** --- evaluating a single pre-season
    component order in a supplier--integrator relationship and examining
    how inventory decisions affect Flextrola and its supplier,
    Solectrics, differently.

Rather than relying on a single deterministic forecast, the models
simulate thousands of possible market outcomes and evaluate alternative
decisions through their resulting distributions of profit and
operational performance.

---

## Business Questions

The project addresses several practical decision questions:

-   How much inventory should a firm commit before uncertain demand is
    realized?
-   How does order quantity affect expected profit and stockout risk?
-   What is the economic cost of carrying excess inventory?
-   How can Monte Carlo simulation quantify the uncertainty surrounding
    expected financial outcomes?
-   How can Excel Data Tables be used to compare alternative decisions
    systematically?
-   Can different firms in the same supply channel prefer different
    inventory decisions?

---

# Case 1 --- Sales Promotion Inventory Decision

## Business Context

A catalog company plans a two-month furniture promotion and must order
chairs before the selling season begins.

The company faces uncertainty in both **customer demand** and **selling
price**.

### Model Assumptions

  ｜Parameter            ｜                       Assumption｜
  ｜---------------------｜---------------------------------｜
  ｜Base order quantity  ｜                      3,000 chairs｜
  ｜Unit procurement cost｜                             \$175｜
  ｜Demand               ｜               Normal(2,000, 500²)｜
  ｜Selling price        ｜             Uniform(\$200, \$300)｜
  ｜Leftover recovery    ｜     50% of realized selling price｜
  ｜imulation size       ｜                    1,000 seasons｜

Demand is constrained to be nonnegative.

For each simulated season, the model calculates:

**Random Demand → Random Price → Sales → Leftover Inventory → Revenue →
Discount Revenue → Procurement Cost → Total Profit**

A stockout indicator is also recorded whenever simulated demand exceeds
available inventory.

---

## Simulation Model

For each simulation run:

``` text
Demand = MAX(0, NORM.INV(RAND(), μ, σ))

Price = Lower Bound + (Upper Bound − Lower Bound) × RAND()

Sales = MIN(Demand, Order Quantity)

Leftover Inventory = Order Quantity − Sales

Total Profit
= Sales Revenue
+ Discount Revenue
− Procurement Cost
```

The simulation produces a distribution of possible profits rather than a
single deterministic estimate.

The model then summarizes:

-   Expected profit
-   95% confidence interval for mean profit
-   Stockout probability
-   Profit distribution
-   Sensitivity to alternative order quantities

---

## Decision Analysis

A one-way Excel **What-If Data Table** evaluates order quantities from:

``` text
S = 500, 600, 700, ..., 3,500
```

For each candidate inventory level, the model estimates:

-   Expected total profit
-   Stockout probability

This allows the inventory decision to be evaluated as a
**profit--service trade-off**.

In the saved simulation results, the highest estimated expected profit
on the tested grid occurs around:

**S = 1,900**

with estimated expected profit of approximately:

**\$125,644**

The analysis also shows that increasing inventory reduces stockout risk
but does not necessarily increase expected profit. Beyond the attractive
inventory region, additional units create greater exposure to discounted
leftover inventory.

---

# Case 2 --- Flextrola Channel Inventory Decision

## Business Context

Flextrola is an electronics systems integrator preparing a component for
a next-generation product with supplier **Solectrics**.

Because the product has a short life cycle and the supplier has a long
lead time, Flextrola has only **one opportunity to place an order before
the selling season**.

### Model Assumptions

  ｜Parameter                     ｜           Value｜
  ｜------------------------------｜ ---------------｜
  ｜Mean demand                   ｜     1,000 units｜
  ｜Demand standard deviation     ｜       600 units｜
  ｜Solectrics production cost    ｜            \$52｜
  ｜Wholesale price to Flextrola  ｜            \$72｜
  ｜Flextrola retail price        ｜           \$121｜
  ｜Secondary-market value        ｜            \$50｜
  ｜Base order quantity           ｜     1,200 units｜
  ｜Simulation size               ｜   5,000 seasons｜

The implemented model constrains simulated demand to be nonnegative.

---

## Performance Measures

For each simulated season, the model calculates:

-   Demand
-   Sales
-   Leftover inventory
-   Sales revenue
-   Secondary-market revenue
-   Procurement cost
-   Flextrola profit
-   Stockout indicator
-   Fill rate
-   Gross margin percentage
-   Solectrics profit

The model also calculates a **95% confidence interval** around estimated
Flextrola mean profit.

At the base order quantity of **1,200 units**, the saved simulation
produces a high average fill rate while also showing meaningful stockout
exposure, illustrating an important distinction:

> A firm can experience stockouts in a substantial fraction of seasons
> while still satisfying a high proportion of total demand on average.

---

## Order-Quantity Sensitivity Analysis

The model evaluates:

``` text
S = 1,000, 1,100, 1,200, ..., 1,600
```

The Data Table tracks Flextrola's expected profit and corresponding
confidence intervals across the decision grid.

### Flextrola

In the saved simulation results, the highest estimated **Flextrola mean
profit** occurs at:

**S = 1,400**

with expected profit of approximately:

**\$34,516.71**

### Solectrics

Solectrics has a different economic objective.

Its unit contribution is:

``` text
$72 wholesale price − $52 production cost = $20 per unit
```

Therefore, supplier profit increases with the quantity ordered by
Flextrola.

Within the tested decision range, Solectrics' maximum profit occurs at:

**S = 1,600**

with supplier profit of:

**\$32,000**

---

# Channel Incentive Misalignment

One of the most important findings of the project is that the two firms
do not necessarily prefer the same inventory decision.

``` text
Flextrola:
Higher inventory
→ fewer lost sales
→ but greater leftover-inventory exposure

Solectrics:
Higher Flextrola order
→ greater supplier sales
→ higher supplier profit
```

Flextrola bears the downside of excess inventory because it purchases
each component for **\$72** but can recover only **\$50** for an unsold
unit.

Solectrics, by contrast, earns a positive contribution on every unit
ordered.

The saved simulation therefore illustrates a **channel incentive
misalignment**:

  ｜Decision Perspective        ｜   Saved Preferred Quantity｜
  ｜----------------------------｜ --------------------------｜
  ｜Flextrola expected profit   ｜                  **1,400**｜
  ｜Solectrics supplier profit  ｜                  **1,600**｜

This distinction demonstrates why an inventory decision that is
attractive to one channel member may not maximize the economic objective
of another.

It also motivates broader supply-chain questions involving **risk
sharing, contract design, buyback arrangements, quantity flexibility,
and channel coordination**.

---

# Analytical Workflow

``` text
Business Problem
      ↓
Define Decision Variable
      ↓
Identify Uncertain Inputs
      ↓
Specify Probability Distributions
      ↓
Generate Random Scenarios
      ↓
Calculate Operational Outcomes
      ↓
Calculate Financial Outcomes
      ↓
Estimate Expected Performance
      ↓
Quantify Simulation Uncertainty
      ↓
Run Data Table Sensitivity Analysis
      ↓
Compare Alternative Decisions
      ↓
Interpret Managerial Trade-offs
```

This separates the core components of the model:

**Inputs → Simulation → Outputs → Decision Analysis**

---

# Excel Techniques Demonstrated

-   Monte Carlo simulation
-   `RAND()`
-   `NORM.INV()`
-   Normal and Uniform random-variable generation
-   Nonnegative demand truncation
-   `IF()`-based operational logic
-   Named Ranges
-   Expected-value estimation
-   `STDEV.S()`
-   95% confidence intervals
-   Stockout probability estimation
-   Fill-rate analysis
-   Gross-margin analysis
-   Profit-distribution analysis
-   Excel What-If **Data Tables**
-   Sensitivity analysis
-   `MAX()` / `LARGE()`
-   `MATCH()`
-   `INDEX()`
-   Simulation-based decision comparison
-   Business-oriented visualization

---

# Key Takeaways

**1. Expected demand alone is insufficient for inventory decisions.**\
A deterministic forecast does not capture stockout risk, excess
inventory, or the distribution of financial outcomes.

**2. Higher service levels are not automatically more profitable.**\
Additional inventory reduces stockouts but increases exposure to
leftover inventory and salvage losses.

**3. Simulation turns uncertainty into measurable decision
information.**\
Instead of generating one forecast, Monte Carlo simulation produces
distributions, probabilities, expected values, and confidence intervals.

**4. Optimization under uncertainty should be interpreted carefully.**\
Because the workbook uses `RAND()`-based simulation, recalculation can
change individual estimates. Small differences between neighboring order
quantities should therefore not be interpreted as exact structural
differences.

**5. The decision maker matters.**\
Flextrola and Solectrics have different profit functions and therefore
can prefer different order quantities.

---

# Model Limitations

-   Distribution parameters are treated as known.
-   Simulated seasons are modeled independently.
-   The models use a single pre-season inventory decision.
-   Lead-time uncertainty and replenishment are not modeled.
-   The Sales Promotion model assumes all leftover inventory can be
    liquidated at 50% of the realized selling price.
-   The Flextrola model assumes a fixed wholesale price and fixed
    secondary-market value.
-   Contract terms between Flextrola and Solectrics are not optimized.
-   `RAND()`-based Data Tables introduce simulation variation across
    recalculations.

Accordingly, individual simulated point estimates should be interpreted
together with sensitivity patterns, confidence intervals, and the
economic structure of the model.

---

# Repository Files

``` text
├── 02_Sales_Promotion_Channel_Management_Portfolio_Project.xlsx
├── 02_Sales_Promotion_Channel_Management_Portfolio_Report.pdf
└── README.md
```

### Excel Workbook

Contains the complete simulation models, random-variable generation,
operational and financial calculations, Data Tables, decision analysis,
visualizations, and interpretation.

### Portfolio Report

Provides a research-style discussion of the business problems,
theoretical framework, simulation methodology, empirical results,
limitations, and managerial implications.

---

# Project Focus

**Business Analytics · Operations Analytics · Monte Carlo Simulation ·
Inventory Management · Decision Analysis · Supply Chain Management ·
Channel Coordination · Excel Modeling**

---

## Author

**Keman Xiang**

*PhD Application Portfolio*

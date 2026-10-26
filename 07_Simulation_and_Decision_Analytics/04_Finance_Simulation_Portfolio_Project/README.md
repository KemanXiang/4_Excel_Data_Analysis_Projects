# Monte Carlo Simulation for Financial Decision-Making

**Investment Withdrawal Strategies and Insurance Loss-Ratio Risk**

This portfolio project uses spreadsheet-based Monte Carlo simulation to analyze two financial decision problems under uncertainty: investment-fund longevity under alternative withdrawal policies and annual insurance loss-ratio risk. Instead of relying on deterministic point estimates, the models generate empirical outcome distributions and evaluate expected outcomes, variability, confidence intervals, tail probabilities, and simulation convergence.

The project was developed in **MGT239: Simulation for Business** and demonstrates the translation of business problems into stochastic models, implementation of simulation logic in Excel, output analysis, and interpretation of results for managerial decision-making.

## Project Overview

|Title|Description|
|---|---|
|Project|Monte Carlo Simulation for Financial Decision-Making|
|Application 1|Investment withdrawal strategy simulation|
|Application 2|Insurance loss-ratio risk simulation|
|Primary Tool|Microsoft Excel|
|Methods|Monte Carlo simulation, stochastic modeling, geometric Brownian motion, random sample size, output analysis, convergence analysis|
|Investment Replications|2,000 simulated paths per withdrawal strategy|
|Insurance Replications|500 simulated years|
|Primary Outputs|Fund life, loss ratio, standard deviation, confidence intervals, tail probabilities, empirical distributions, convergence diagnostics|

## Business Questions

The project addresses two related questions:

1. **Investment strategy:** How does the order in which stock and bond assets are withdrawn affect the distribution of time until an investment fund is depleted?
2. **Insurance risk:** How do stochastic policy volume, coverage, claim occurrence, and claim severity combine to determine annual loss ratios and the probability that losses exceed premiums?

These problems require simulation because their outcomes emerge from interacting random variables and, in the investment case, from a dynamic path-dependent process.

---

## Part I — Investment Withdrawal Strategy Simulation

### Problem

A **$1,000,000 fund** begins with equal allocations to stocks and bonds.

|Parameter|Value|
|---|---|
|Initial stock fund|$500,000|
|Initial bond fund|$500,000|
|Annual stock drift|8%|
|Annual stock volatility|12%|
|Annual bond return|5%|
|Annual withdrawal|$120,000|
|Simulation time step|1 year|
|Maximum path horizon|50 years|
|Monte Carlo replications|2,000 per strategy|

Two withdrawal policies are compared.

**Parallel withdrawal:** $60,000 is withdrawn from stocks and $60,000 from bonds each year. If one account cannot provide its scheduled share, the remaining amount is withdrawn from the other account.

**Bond-first withdrawal:** the $120,000 annual withdrawal is taken from bonds first. Once bonds are insufficient, the remaining withdrawal is taken from stocks.

The primary outcome is the **stopping time**, or the number of years until the combined fund is depleted.

### Stochastic Model

The stock portfolio follows a discrete-time geometric Brownian motion process. For each annual period, the stochastic growth factor is:

`exp[(μ − σ²/2)Δt + σ√Δt Z]`, where `Z ~ N(0,1)`.

The bond account grows deterministically at the fixed annual rate after withdrawals. Because each year's ending balances determine the next year's starting balances, this model is **path-dependent**. Each Monte Carlo replication represents a complete simulated sample path.

### Simulation Workflow

`Initial Portfolio → Annual Withdrawal → Stock/Bond State Update → Random Stock Return → Remaining Fund → Alive Indicator → Stopping Time`

The process is repeated 2,000 times for each strategy, producing empirical distributions of fund life.

### Investment Results

|Metric|Parallel Withdrawal|Bond-First Withdrawal|
|---|---|---|
|Mean fund life|11.9445 years|12.5695 years|
|Standard deviation|1.5634|2.3062|
|95% CI for mean|[11.8760, 12.0130]|[12.4684, 12.6706]|
|Minimum observed fund life|9 years|8 years|
|Maximum observed fund life|33 years|30 years|
|Difference in mean fund life|—|+0.6250 years|

Under the modeled assumptions, the **bond-first strategy increases expected fund life by approximately 0.625 years**, equivalent to roughly **7.5 months**.

The result reflects the sequencing of asset exposure. By withdrawing from bonds first, a larger portion of the stock portfolio remains invested for longer, allowing the higher assumed stock drift to compound over additional periods.

However, the bond-first strategy also produces greater dispersion. Its standard deviation is higher, and its minimum observed fund life is lower. The strategy with the higher expected longevity therefore does not dominate the alternative in every individual simulation path.

### Investment Convergence

|Replications|Parallel Mean|Bond-First Mean|Difference|
|---|---|---|---|
|50|11.8400|11.8600|0.0200|
|100|12.2200|12.1200|-0.1000|
|250|12.0480|12.2040|0.1560|
|500|11.9800|12.3940|0.4140|
|1,000|11.9430|12.4880|0.5450|
|1,500|11.9507|12.5600|0.6093|
|2,000|11.9445|12.5695|0.6250|

The convergence analysis shows why policy conclusions should not be based on a small number of simulation runs. At 100 replications, the apparent ordering temporarily reverses. As additional paths are simulated, the bond-first advantage becomes increasingly stable.

This directly illustrates **Monte Carlo sampling error** and the importance of checking convergence before interpreting simulation results.

---

## Part II — Insurance Loss-Ratio Risk Simulation

### Problem

The insurance model evaluates annual performance when multiple sources of uncertainty interact.

The primary outcome is the annual **loss ratio**:

`R = Total Loss / Total Premium`

A year with `R > 1` represents an adverse outcome in which total losses exceed total premiums.

### Stochastic Inputs

|Component|Model Assumption|
|---|---|
|Annual policy sales S|Normal distribution, mean = 100, SD = 10|
|Basic liability X|Uniform distribution on [50, 200]|
|Excess coverage|Purchased with probability 0.40|
|Excess liability amount|0.2X|
|Claim occurrence|Bernoulli process with probability p_c|
|Claim severity|Exponential distribution with mean r_c × premium|
|Monte Carlo horizon|500 simulated years|

### Random Sample Size

Annual policy volume is itself random. The spreadsheet handles this using a fixed capacity of potential policies and an indicator:

`pick = 1(ID ≤ S)`

Only policies whose IDs fall within the simulated annual sales count are included in realized premium and loss totals. This technique allows a fixed spreadsheet structure to represent a **random sample size**.

### Frequency-Severity Scenarios

|Scenario|Severity Parameter r_c|Claim Probability p_c|r_c × p_c|
|---|---|---|---|
|1|5|0.16|0.80|
|2|10|0.08|0.80|
|3|20|0.04|0.80|
|4|80|0.01|0.80|

Holding `r_c × p_c` constant provides a controlled framework for examining how similar expected loss intensity can coexist with different levels of volatility and tail risk.

### Insurance Simulation Workflow

`Annual Policy Sales → Policy Coverage → Excess Coverage Decision → Premium → Claim Occurrence → Claim Severity → Total Premium & Loss → Loss Ratio`

This process is repeated across **500 simulated years**.

### Insurance Results

|Metric|Simulation Result|
|---|---|
|Mean loss ratio|0.836676|
|Standard deviation|0.890527|
|Minimum observed loss ratio|0.000656|
|Maximum observed loss ratio|7.391006|
|Probability R > 1|29.4%|
|Standard error of mean|0.039826|

The simulated mean loss ratio is below one, but the distribution is highly dispersed. Most importantly, **29.4% of simulated years have a loss ratio greater than one**.

The maximum simulated loss ratio is substantially above both the mean and the threshold of one, demonstrating pronounced right-tail exposure. Because claim severity follows an exponential distribution, occasional severe claims can have a disproportionate effect on annual aggregate losses.

The result illustrates an important risk-management principle: **an acceptable expected value does not imply low downside risk**.

### Insurance Convergence

|Simulated Years|Running Mean R|Running P(R > 1)|
|---|---|---|
|25|1.1577|32.0%|
|50|0.9819|30.0%|
|100|0.9771|35.0%|
|200|0.8636|31.0%|
|300|0.9063|31.0%|
|400|0.8446|29.8%|
|500|0.8367|29.4%|

The estimates fluctuate substantially at smaller sample sizes because rare, high-severity claims can strongly influence the running average. As the number of simulated years increases, the estimates become more stable.

---

## Analytical and Managerial Insights

|Dimension|Investment Model|Insurance Model|
|---|---|---|
|System Type|Dynamic, path-dependent system|Aggregate annual risk system|
|Primary Uncertainty|Stock returns|Policy volume, coverage, claims, severity|
|Key Outcome|Fund depletion time|Annual loss ratio|
|Decision Focus|Compare withdrawal policies|Evaluate performance and tail risk|
|Important Distributional Measure|Stopping-time distribution|P(R > 1) and right-tail behavior|
|Simulation Diagnostic|Running mean fund life|Running mean R and P(R > 1)|

Several broader conclusions emerge:

- **Distributional analysis is more informative than mean-only analysis.** The investment strategy with the higher expected fund life also has greater dispersion. Similarly, the insurance model has a mean loss ratio below one while still producing a substantial probability of losses exceeding premiums.
- **Decision rules can change outcomes even when total cash requirements remain unchanged.** Both investment strategies withdraw the same annual amount, but withdrawal sequencing changes the amount of capital remaining exposed to stochastic stock growth.
- **Frequency and severity should be evaluated separately.** Similar expected loss intensity can coexist with different risk distributions when the balance between claim frequency and claim severity changes.
- **Convergence should be examined before interpreting Monte Carlo results.** Small simulation samples can produce unstable estimates or temporary reversals in apparent policy comparisons.
- **Simulation supports decision-making by preserving uncertainty.** The models propagate uncertainty through the complete business system rather than replacing uncertain inputs with averages.

---

## Limitations

The simulation results are conditional on the assumptions embedded in the workbook.

For the investment model, the stock process assumes constant drift and volatility, annual Normal shocks within a geometric Brownian motion framework, a fixed bond return, fixed nominal withdrawals, and no taxes, transaction costs, fees, inflation, or market-regime changes.

For the insurance model, policy outcomes follow the specified Normal, Uniform, Bernoulli, and Exponential distributions. The model does not incorporate correlated claims, heterogeneous underwriting classes, deductibles, reinsurance, inflation, pricing adaptation, or multi-year learning.

Increasing the number of Monte Carlo replications reduces simulation sampling error but does not by itself validate the structural assumptions.

---

## Repository Contents

|File / Component|Purpose|
|---|---|
|Finance Simulation Portfolio Excel Workbook|Complete simulation models, calculation sheets, output analysis, visualizations, and convergence analysis|
|Portfolio Report|Research-style documentation of the problem, methodology, results, interpretation, managerial implications, and limitations|
|README.md|Concise project overview and repository guide|

### Workbook Structure

|Worksheet|Purpose|
|---|---|
|Portfolio Overview|Project summary and navigation|
|1_Investment_Stategy1|Parallel-withdrawal simulation engine|
|1_Investment_Stategy2|Bond-first simulation engine|
|2_Insurance|Insurance simulation engine|
|Investment Analysis|Investment output analysis and interpretation|
|Insurance Analysis|Insurance output analysis and interpretation|
|Convergence|Monte Carlo convergence diagnostics|

---

## Skills Demonstrated

- Monte Carlo simulation
- Stochastic business modeling
- Geometric Brownian motion
- Dynamic state-transition modeling
- Stopping-time analysis
- Random-variable generation
- Random sample-size simulation
- Insurance frequency-severity modeling
- Empirical distribution analysis
- Confidence intervals and standard errors
- Tail-probability estimation
- Simulation convergence diagnostics
- Excel Data Tables and formula-based simulation
- Business interpretation of quantitative results
- Reproducible spreadsheet documentation

---

## Portfolio Relevance

This project demonstrates the ability to move from a business decision problem to a formal stochastic model, implement the model in Excel, generate and analyze Monte Carlo outcomes, evaluate simulation precision, and translate quantitative results into decision-relevant insights.

The investment and insurance applications are intentionally different in structure. One emphasizes **dynamic stochastic processes, path dependence, and policy comparison**, while the other emphasizes **multiple random variables, random sample size, aggregate risk, and tail probabilities**. Together, they provide a broader demonstration of simulation-based analytical reasoning than either model would provide independently.

---

## Author

**Keman Xiang**

*MGT239 Simulation for Business Portfolio Project*  
*Keman Xiang PhD Application Portfolio*

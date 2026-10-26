# Dynamic Financial Simulation: Asian Option Pricing and Protective-Put Hedging

## Project Overview

This project applies **Monte Carlo simulation** to two connected
financial problems: the valuation of path-dependent Asian options and
the evaluation of a protective-put hedging strategy. Stock prices are
modeled as a dynamic stochastic system using a geometric random walk.
The analysis then translates simulated market outcomes into derivative
payoffs, empirical distributions, confidence intervals, downside-risk
measures, and an explicit hedging decision.

The project demonstrates how simulation can move beyond a single
expected value and support financial decision-making through **sample
paths, payoff distributions, risk measures, and convergence
diagnostics**.

|Project Component|Description|
|---|---|
|Course|MGT239 Simulation for Business|
|Method|Monte Carlo simulation and dynamic stochastic modeling|
|Financial Model|Geometric random walk / discrete-time Brownian-motion framework|
|Module 1|Path-dependent Asian call and put valuation|
|Module 2|Protective-put hedging and risk comparison|
|Asian Option Simulation|1,000 one-year weekly stock-price paths|
|Hedging Simulation|2,000 six-month terminal-price scenarios|
|Core Outputs|Expected discounted payoff, 95% confidence intervals, payoff probabilities, variance, downside risk, payoff distributions, and convergence diagnostics|
|Final Hedging Decision|**No Hedging** under the decision criterion used in Q3|
## Business Problem

Financial outcomes evolve over time under uncertainty. A stock price
next period depends on its current state and a new random shock, so many
financial decisions require modeling an entire sequence of possible
states rather than a single static observation.

This project addresses two questions:

1.  **Asian option valuation:** How can Monte Carlo simulation estimate
    the payoff distribution and expected discounted payoff of an option
    whose value depends on the average stock price over time?
2.  **Financial hedging:** Does purchasing a European put improve the
    simulated risk profile enough to justify hedging the stock position
    under the project's decision criterion?

## Theoretical Framework

### Dynamic Systems and Sample Paths

Let (S_t) denote the stock price at time (t). The stock-price process is
simulated recursively as:

`S_t = S_(t-1) * EXP((mu - sigma^2 / 2) * Delta_t + sigma * SQRT(Delta_t) * Z_t)`, where `Z_t ~ N(0,1)`

A single Monte Carlo replication of the Asian-option model therefore
produces an entire **sample path**, not just one random number. With
weekly observations over one year, each simulated path contains the
sequence of stock prices needed to calculate the average asset price.

### Asian Option Payoffs

For each simulated path, the arithmetic average stock price is used to
calculate discounted Asian-option payoffs:

`Asian Call Payoff = MAX(S_avg - K, 0) * EXP(-r * T)`

`Asian Put Payoff = MAX(K - S_avg, 0) * EXP(-r * T)`

Because the payoff depends on (S\_{avg}), the Asian option is **path
dependent**.

### Protective-Put Hedging

The hedging module compares:

-   **Strategy 1 --- No Hedging:** hold the stock without downside
    protection.
-   **Strategy 2 --- Hedging:** hold the stock and purchase a European
    put for a premium of 0.57.

The two strategies are evaluated using the same simulated market
scenarios so that differences in their payoff distributions reflect the
effect of the hedge.

## Simulation Design

### Asian Option Model

  Parameter                      Value

|Parameter|Value|
|---|---|
|Initial stock price `S0`|100|
|Drift `mu`|0.08|
|Volatility `sigma`|0.12|
|Strike price `K`|97|
|Expiration `T`|1 year|
|Step size `Delta_t`|1/52 year|
|Risk-free rate `r`|0.059|
|Monte Carlo paths `N`|1,000|

Each run generates a weekly stock-price trajectory, calculates the
path-average stock price, and converts that average into discounted
Asian call and put payoffs. The 1,000 replications are then used to
estimate payoff distributions, expected discounted payoffs, confidence
intervals, and payoff probabilities.

### Hedging Model

  Parameter                      Value

|Parameter|Value|
|---|---|
|Initial stock price `S0`|100|
|Drift `mu`|0.08|
|Volatility `sigma`|0.12|
|Put strike `K`|97|
|Expiration `T`|0.5 year|
|Step size `Delta_t`|0.5 year|
|Risk-free rate `r`|0.059|
|Monte Carlo replications `N`|2,000|
|Put premium `c`|0.57|

Each run generates a six-month terminal stock price and calculates the
payoff of the stock-only position, the European put, and the
stock-plus-put position.

## Key Results

### Asian Option Simulation

  Metric                    Asian Put            Asian Call

|Metric|Asian Put|Asian Call|
|---|---|---|
|Mean discounted payoff|0.4651|7.9093|
|95% confidence interval|[0.3716, 0.5585]|[7.5089, 8.3098]|
|P(payoff > 1.1)|11.50%|81.60%|
|95% CI for probability|[9.51%, 13.49%]|[79.20%, 84.00%]|

The simulated put payoff distribution contains a large concentration at
zero, while the call produces a much broader positive-payoff
distribution. Under the workbook assumptions, many simulated average
stock prices remain above the strike price of 97, producing
substantially more favorable call outcomes than put outcomes.

### Hedging Simulation

The 2,000 simulated scenarios produce a mean terminal stock price of
**104.0656**. The estimated probability that the terminal stock price
falls below the initial price is **33.45%**.

The simulated discounted European put payoff has a mean of **0.9674**
with a 95% confidence interval of **`[0.8594, 1.0754]`**. The workbook's
quoted put premium of **0.57** lies below this simulation interval.
These values should be interpreted as expected discounted payoffs under
the workbook's specified model assumptions rather than as a claim of an
arbitrage-free market price.
|Risk / Payoff Metric|Stock Only|Stock + Put|
|---|---|---|
|Mean discounted payoff|3.9474|4.3448|
|Payoff variance|73.6949|52.4710|
|Probability of negative payoff|33.45%|36.50%|
|Maximum simulated payoff|38.9130|38.3430|
|Minimum simulated payoff|-23.7938|-3.4828|
The protective put reduces payoff variance by approximately **28.8%**
and sharply improves the worst simulated payoff. However, the
probability of a negative payoff increases from **33.45% to 36.50%**,
while the hedge also requires payment of the **0.57 option premium**.

### Q3 Decision: No Hedging

The simulation reveals a trade-off rather than an unconditional benefit
from hedging. The put clearly reduces the **severity and dispersion of
losses**, but it does not reduce the downside-risk probability used in
the project's Q3 decision.

Under the decision criterion implemented in the workbook, the result is
therefore:

> **No Hedging**

This does **not** imply that the put provides no protection. Instead,
the result shows that protection against severe losses comes at a cost
and does not improve the particular downside-risk measure used to make
the final decision.

## Monte Carlo Convergence

Running means are calculated at regular checkpoints to evaluate whether
the simulation estimates become more stable as the number of
replications increases.

For the Asian options, the running means fluctuate substantially at
small sample sizes and become progressively more stable as the
simulation approaches 1,000 paths. The hedging estimates show the same
pattern across 2,000 replications.

The convergence analysis provides an additional diagnostic that the
final estimates are not determined only by a small number of early
random draws.

## Analytical and Business Insights

**Path dependence matters.** For an Asian option, the terminal stock
price alone is insufficient because the payoff depends on the average
price across the entire trajectory.

**A distribution is more informative than a point estimate.** Expected
payoff alone does not reveal the probability of zero payoff, tail
behavior, payoff dispersion, or simulation uncertainty.

**Risk measures can point in different directions.** The protective put
reduces variance and extreme-loss severity while increasing the
probability of a small negative payoff. A hedging decision therefore
depends on the specific risk objective being optimized.

**Insurance has a cost.** The put premium shifts the hedged payoff
distribution downward in scenarios where the protection is not
sufficiently valuable. Downside protection should therefore be evaluated
against its cost rather than assumed to be preferable automatically.

**Monte Carlo convergence matters.** Tracking running estimates helps
distinguish a relatively stable simulation estimate from one that
remains highly sensitive to the number of replications.

## Limitations

The results are conditional on the assumptions implemented in the Excel
model. The stock process assumes constant drift and volatility,
independent standard-normal shocks, and a geometric random walk. Real
financial markets can exhibit changing volatility, jumps, dependence,
liquidity effects, transaction costs, and parameter uncertainty.

The workbook also generates stock-price paths using (mu=0.08)
while discounting payoffs at (r=0.059). Accordingly, the option results
are described as **Monte Carlo expected discounted payoffs under the
specified model assumptions**, rather than as strict arbitrage-free
risk-neutral prices.

Finally, Monte Carlo estimates contain sampling error. Recalculating the
workbook can produce somewhat different numerical results because the
simulation is driven by random draws.

## Project Workflow

``` text
Define financial assumptions
        ↓
Generate stochastic stock-price outcomes
        ↓
Asian Option                         Hedging
52-week sample paths                 6-month terminal prices
        ↓                                   ↓
Average stock price                  Stock / put payoffs
        ↓                                   ↓
Call & put payoffs                   Compare two strategies
        ↓                                   ↓
Distributions & CIs                  Mean / variance / downside risk
        ↓                                   ↓
Monte Carlo convergence              Q3 decision: No Hedging
```

## Repository Files

|File|Purpose|
|---|---|
|`3_Dynamic_Simulation_Option_Pricing_Hedging_Portfolio_Project.xlsx`|Complete Excel simulation model, calculations, charts, results, interpretation, and convergence diagnostics|
|`3_Dynamic_Financial_Simulation_Portfolio_Report.pdf`|Research-style project report covering theory, methodology, simulation results, interpretation, limitations, and business implications|
|`README.md`|Concise project overview and entry point for the GitHub repository|

## Skills Demonstrated

-   Monte Carlo simulation
-   Dynamic stochastic systems
-   Sample-path simulation
-   Geometric random walk
-   Financial derivative modeling
-   Path-dependent Asian option analysis
-   European put payoff analysis
-   Confidence-interval estimation
-   Distributional risk analysis
-   Protective-put hedging
-   Variance and downside-risk comparison
-   Monte Carlo convergence diagnostics
-   Excel-based simulation modeling
-   Financial decision analysis

## Conclusion

This project demonstrates how Monte Carlo simulation can connect
**dynamic financial uncertainty, derivative valuation, and
risk-management decisions**. The Asian-option analysis shows why
path-dependent financial products require simulation of complete price
trajectories. The hedging analysis shows that a derivative can
materially reduce payoff variance and severe-loss exposure without
necessarily improving every risk metric.

Most importantly, the final hedging decision is tied to the model's
explicit criterion. Although the protective put reduces variance and
substantially limits the worst simulated losses, the probability of a
negative payoff increases from 33.45% to 36.50% and the strategy
requires an option premium. Under the Q3 decision rule, the simulation
therefore supports **No Hedging**.

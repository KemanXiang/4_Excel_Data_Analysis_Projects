# Bass Diffusion & Product Life-Cycle Simulation

## Project Overview

This project applies a **stochastic Bass diffusion model** and **Monte Carlo simulation** to analyze the life cycle of a new product, Q-Phone. The objective is to understand **how adoption evolves over time**, determine **when sales reach maturity and enter decline**, and translate those dynamics into a **practical product-rollover decision**.

The project illustrates an important managerial distinction: **declining monthly sales do not necessarily indicate deteriorating execution**. Under a finite-market diffusion process, sales can decline naturally as cumulative adoption rises and the remaining pool of potential adopters shrinks.

The Excel model simulates a 60-month product life cycle and replicates the process across **1,000 stochastic life cycles** to estimate the timing and uncertainty of key lifecycle milestones.

## Business Problem

Q-Phone is modeled as a newly launched durable product with an estimated addressable market of **1,000,000 consumers**. The analysis asks **how a representative product life cycle evolves, when maturity and decline begin, how long maturity lasts, when the next generation should be introduced, and how diffusion assumptions affect these outcomes**.

## Theoretical Framework

The **Bass diffusion model** represents adoption through innovation (`p`) and imitation (`q`). The discrete-time adoption probability used in the project is:

**fₜ = (1 − Fₜ)(p + qFₜ)**

|Symbol|Definition|
|---|---|
|`m`|Total market potential|
|`Mₜ`|Remaining market potential at month `t`|
|`Xₜ`|Sales during month `t`|
|`Nₜ`|Cumulative adopters through month `t`|
|`Fₜ`|Fraction of the market adopted (`Nₜ / m`)|
|`fₜ`|Period adoption probability|
|`p`|Innovation rate|
|`q`|Imitation / contagion rate|

The stochastic transition is represented as **Mₜ₊₁ ~ Binomial(Mₜ, 1 − fₜ)**, with `Nₜ = m − Mₜ`, `Xₜ = Nₜ − Nₜ₋₁`, and `Fₜ = Nₜ / m`.

## Simulation Design

|Parameter|Value|Interpretation|
|---|---:|---|
|Market potential (`m`)|1,000,000|Maximum potential adopters|
|Innovation rate (`p`)|0.01|Intrinsic adoption force|
|Imitation rate (`q`)|0.20|Social / contagion effect|
|Simulation horizon (`T`)|60 months|Product life-cycle window|
|Monte Carlo replications (`N`)|1,000|Simulated product life cycles|

The project contains four analytical stages:

1. **Single lifecycle simulation** — tracks remaining prospects, monthly sales, cumulative adoption, penetration, and adoption probability across 60 months.
2. **Monte Carlo lifecycle analysis** — replicates the model 1,000 times to estimate maturity, decline, and mature-stage duration.
3. **Product rollover analysis** — estimates the latest timing benchmark for introducing the next generation before decline.
4. **Sensitivity analysis** — varies market potential, innovation, and imitation to examine changes in diffusion behavior.

## Lifecycle Metrics

|Metric|Definition|
|---|---|
|`tₚ`|Peak-sales month / beginning of maturity|
|`t_d`|Beginning of decline, defined by the model as reaching the 80% cumulative-adoption threshold|
|`d`|Mature-stage duration (`t_d − tₚ`)|
|Latest rollover timing|Latest modeled launch benchmark before the decline stage|

## Key Results

Across **1,000 simulated product life cycles**, the workbook produces:

|Lifecycle Metric|Mean (Months)|95% CI Low|95% CI High|
|---|---:|---:|---:|
|Peak / maturity start (`tₚ`)|15.116|15.085|15.147|
|Decline-stage start (`t_d`)|39.488|39.457|39.519|
|Mature-stage duration (`d`)|24.372|24.329|24.415|
|Latest rollover benchmark|38.486|38.455|38.517|

The simulations indicate that the product typically reaches peak monthly sales around **month 15**, reaches the modeled decline threshold around **month 39–40**, and remains in the mature stage for approximately **24 months**. The mean latest product-rollover benchmark is approximately **month 38.5**.

## Representative Product Life Cycle

The representative 60-month path in the workbook demonstrates the mechanism underlying the Bass diffusion process. Monthly sales initially rise as imitation strengthens, peak, and subsequently decline as the remaining market potential becomes smaller.

In this sample path, monthly sales peak at approximately **34,514 units in month 15**. Cumulative adoption at the peak is approximately **331,341 consumers**, or **33.13% of the modeled market**. By approximately month 40, cumulative adoption exceeds the model's 80% decline-stage threshold.

These figures describe one stochastic realization. The 1,000-run results provide the primary basis for lifecycle timing conclusions.

## Simulation Convergence

Running estimates were calculated at increasing simulation sizes to evaluate Monte Carlo precision.

|Simulation Runs|Mean Peak Month|Mean Decline Month|Mean Mature Duration|
|---|---:|---:|---:|
|25|15.240|39.480|24.240|
|50|15.100|39.460|24.360|
|100|15.070|39.500|24.430|
|250|15.140|39.504|24.364|
|500|15.124|39.506|24.382|
|750|15.127|39.489|24.363|
|1,000|15.116|39.488|24.372|

The estimates become increasingly stable as the number of simulated life cycles grows. This convergence supports the use of **1,000 replications** as a stable basis for estimating mean lifecycle timing under the specified model assumptions.

## Sensitivity Analysis

The parameter experiments distinguish **market scale** from **diffusion dynamics**.

Increasing market potential primarily changes sales volume rather than the lifecycle timing structure under the baseline diffusion parameters. Changes in innovation (`p`) and imitation (`q`) alter the diffusion mechanism more directly, although the timing metrics remain relatively stable across the particular parameter ranges tested in this workbook.

The sensitivity results should therefore be interpreted within the tested simulation scenarios rather than as a general claim that the diffusion coefficients are unimportant.

## Interpretation

The model reproduces the product-life-cycle sequence:

**Introduction → Acceleration → Peak → Maturity → Decline**

Early adoption is initiated by innovation. As cumulative adoption grows, imitation strengthens and accelerates sales. Eventually, however, the remaining pool of prospects becomes increasingly limited. Monthly sales can therefore decline even while cumulative adoption continues to increase.

The result demonstrates why a decline in monthly sales can be **endogenous to diffusion and market saturation**, rather than automatically indicating poor marketing execution or declining product quality.

## Managerial Implications

### Lifecycle Diagnosis

Managers should evaluate sales trends together with cumulative market penetration. Falling monthly sales may represent a natural transition toward saturation rather than an isolated demand problem.

### Product-Rollover Planning

The modeled decline stage begins around **month 39.5**, while the latest rollover benchmark averages approximately **month 38.5**. The successor product therefore needs to be prepared before decline becomes fully visible in realized sales.

The model does not determine engineering or development lead time. Instead, it provides a **market-side timing benchmark** against which product development, supply-chain preparation, channel readiness, and launch planning can be coordinated.

### Decision-Making Under Uncertainty

A single lifecycle path illustrates diffusion but cannot characterize simulation uncertainty. Monte Carlo replication converts lifecycle events into distributions and makes the stability of timing estimates observable.

## Limitations

The model intentionally simplifies the market. Its assumptions include:

- fixed market potential;
- constant innovation and imitation parameters within a scenario;
- one adoption per consumer;
- no explicit competitor entry;
- no price changes;
- no separate advertising or promotional effects;
- no repeat purchases;
- no capacity constraints;
- no customer heterogeneity;
- no seasonality; and
- no empirical parameter-estimation error.

The **80% cumulative-adoption threshold** is a modeling definition of decline rather than a universal managerial rule.

The reported confidence intervals quantify uncertainty in the **Monte Carlo estimate of mean timing**. They are not prediction intervals for real-world product life cycles.

## Workbook Structure

|Worksheet|Purpose|
|---|---|
|`Project Overview`|Business problem, theoretical framing, simulation design, lifecycle definitions, and analytical questions|
|`Sheet1`|Bass diffusion calculations, stochastic simulation, 60-month sample path, Monte Carlo outputs, rollover analysis, and parameter experiments|
|`Results & Interpretation`|Lifecycle estimates, confidence intervals, convergence analysis, visualizations, and managerial interpretation|

## Project Files

|File|Description|
|---|---|
|`5_Bass_Diffusion_Portfolio_Project.xlsx`|Excel simulation model and portfolio workbook|
|`Bass_Diffusion_Product_Lifecycle_Simulation_Report.pdf`|Research-style project report|
|`README.md`|GitHub project documentation|

## Skills Demonstrated

- Monte Carlo simulation
- Bass diffusion modeling
- stochastic modeling
- product life-cycle analysis
- new-product adoption analysis
- simulation convergence assessment
- sensitivity analysis
- uncertainty interpretation
- Excel simulation modeling
- business analytics
- managerial decision support
- analytical communication

## References

Bass, F. M. (1969). *A New Product Growth for Model Consumer Durables*. **Management Science, 15**(5), 215–227.

Mahajan, V., Muller, E., & Bass, F. M. (1995). *Diffusion of New Products: Empirical Generalizations and Managerial Uses*. **Marketing Science, 14**(3_supplement), G79–G88.

Schmittlein, D. C., & Mahajan, V. (1982). *Maximum Likelihood Estimation for an Innovation Diffusion Model of New Product Acceptance*. **Marketing Science, 1**(1), 57–78.

## Author

**Keman Xiang**

PhD Application Portfolio  
Simulation for Business / Marketing Analytics / Data Analytics

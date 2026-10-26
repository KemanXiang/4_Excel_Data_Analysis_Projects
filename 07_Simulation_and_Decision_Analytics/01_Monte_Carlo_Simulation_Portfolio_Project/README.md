# Monte Carlo Simulation under Uncertainty

## Decision-Rule Evaluation \| Monte Carlo Estimation \| Statistical Precision \| Excel

This project applies **Monte Carlo simulation in Excel** to two
complementary problems involving uncertainty. The first evaluates the
long-run consequences of a threshold-based dinner-payment rule when two
salespeople have different stochastic sales processes. The second uses
randomly generated dart locations to estimate a geometric probability
and recover the value of **π**, while examining how simulation precision
changes as the number of replications increases.

Together, the two cases demonstrate a common simulation framework:

**Uncertain Inputs → Random Sampling → Model Logic → Repeated Trials →
Output Distribution → Statistical Interpretation**

The project emphasizes not only how to generate random variables, but
also how to interpret stochastic outputs, quantify simulation
uncertainty, and translate simulation results into decision-oriented
insights.

---

# Project Objectives

The project addresses several analytical questions:

-   How can uncertain business inputs be represented with probability
    distributions?
-   How can a seemingly neutral threshold rule generate asymmetric
    outcomes?
-   Why should decision rules be evaluated across distributions rather
    than only at expected values?
-   How can Monte Carlo simulation estimate an unknown probability?
-   How does simulation size affect sampling variability and
    confidence-interval precision?
-   Why can a larger simulation produce a more precise estimate even
    when the realized point estimate does not improve monotonically?

---

# Case 1 --- Dinner-Deal Decision Rule

## Business Context

Sam and Mary are salespeople whose weekly sales are uncertain.

Sam's weekly sales (X), measured in thousands of dollars, are modeled
as:

``` text
X ~ Uniform(1, 5)
```

Mary's weekly sales (Y) are modeled as:

``` text
Y ~ Normal(3, 1.3²)
```

Their weekly performance is compared using:

``` text
R = X / Y
```

A threshold-based rule determines who pays for dinner:

``` text
If R < 0.3      → Sam buys
If R > 0.7      → Mary buys
Otherwise        → Split the check
```

The objective is not to predict one particular week. Instead, the model
asks what **distribution of payment outcomes** emerges when this rule is
repeatedly applied under the assumed uncertainty.

---

## Excel Simulation Design

The workbook simulates **200 weeks**.

For each simulated week:

``` text
Sam's Sales = 1 + 4 × RAND()

Mary's Sales = NORM.INV(RAND(), 3, 1.3)

Performance Ratio = Sam's Sales / Mary's Sales
```

The ratio is then converted into one of three mutually exclusive
outcomes:

``` text
1 = Sam buys
2 = Mary buys
3 = Split
```

The resulting frequencies summarize the long-run consequences of the
decision rule.

---

## Saved Simulation Results

In the saved 200-week simulation snapshot:

|Outcome|Frequency|Share|
|---|---|---|
|Sam buys|9|4.5%|
|Mary buys|137|68.5%|
|Split|54|27.0%|

The simulated payment burden is strongly asymmetric: Mary pays much more
frequently than Sam.

If fairness is interpreted as an approximately balanced frequency of
paying for dinner, the saved simulation does not support the rule as
balanced under the stated probability distributions and thresholds.

Because the model is stochastic, the exact counts change when Excel
recalculates. The more important analytical object is the **long-run
outcome distribution implied by the model and decision thresholds**.

---

## Business Interpretation

The case illustrates an important principle in decision analytics:

> A rule that appears neutral in algebraic form can generate
> systematically asymmetric outcomes when applied to heterogeneous
> underlying distributions.

This issue extends beyond the dinner example. Similar threshold-based
rules appear in:

-   incentive systems,
-   performance evaluation,
-   credit classification,
-   supplier scorecards,
-   service-level policies,
-   operational triggers, and
-   resource-allocation rules.

Simulation provides a practical way to **stress-test decision rules
before implementation** by examining the distribution of their
consequences rather than relying only on average inputs.

---

# Case 2 --- Dart Game and Monte Carlo Estimation of π

## Problem Formulation

The second model uses a geometric experiment to demonstrate Monte Carlo
estimation.

Consider a circle of radius 1 positioned inside a 2 × 2 square. If darts
land uniformly at random within the square, the probability of landing
inside the circle is:

``` text
P(Hit) = Area of Circle / Area of Square
       = π / 4
```

Therefore:

``` text
π = 4 × P(Hit)
```

The workbook simulates random dart locations, estimates the probability
of a hit, and then calculates:

``` text
π̂ = 4 × p̂
```

where `p̂` is the simulated proportion of darts landing inside the
circle.

---

## Simulation Logic

The workbook uses one quarter of the geometry.

Each dart receives two independent coordinates:

``` text
X ~ Uniform(0,1)
Y ~ Uniform(0,1)
```

Its distance from the origin is:

``` text
d = √(X² + Y²)
```

The hit indicator is:

``` text
H = 1 if d < 1
H = 0 otherwise
```

The estimated hit probability is the average of the hit indicators:

``` text
p̂ = Average(H)
```

and the corresponding Monte Carlo estimate of π is:

``` text
π̂ = 4p̂
```

---

# Simulation Size and Convergence

Four simulation sizes are compared:

``` text
N = 100
N = 500
N = 1,000
N = 5,000
```

For each sample size, the workbook reports the estimated hit
probability, the implied estimate of π, and an approximate 95%
confidence interval.

## Saved Results

|N|Estimated π|Absolute Error|95% CI Width|
|---|---|---|---|
|100|3.3600|0.2184|0.5777|
|500|3.2000|0.0584|0.2808|
|1,000|3.2200|0.0784|0.1966|
|5,000|3.1144|0.0272|0.0921|

The point estimates do **not** move monotonically toward π. For example,
the estimate at `N = 500` is closer to π than the estimate at
`N = 1,000`.

This is expected in a stochastic experiment.

Increasing the number of trials reduces **sampling variability**, but it
does not guarantee that every individual realization from a larger
simulation will be closer to the true value than every realization from
a smaller simulation.

---

# Confidence Intervals and Simulation Precision

For a simulated Bernoulli hit indicator, the workbook estimates
uncertainty using:

``` text
p̂ ± 1.96 × s / √N
```

Because:

``` text
π̂ = 4p̂
```

the confidence-interval endpoints for π are obtained by multiplying the
probability interval by four.

The strongest convergence pattern appears in the **confidence-interval
width**:

``` text
N = 100      → CI width ≈ 0.578
N = 500      → CI width ≈ 0.281
N = 1,000    → CI width ≈ 0.197
N = 5,000    → CI width ≈ 0.092
```

From `N = 100` to `N = 5,000`, the interval becomes approximately **84%
narrower**.

This demonstrates the approximate square-root relationship between
simulation size and standard error:

``` text
Standard Error ∝ 1 / √N
```

Consequently, simulation precision improves as the number of
replications increases, but the improvement exhibits **diminishing
returns**.

---

# Integrated Analytical Framework

Although the two cases address different questions, they use the same
underlying simulation architecture.

|Simulation Component|Dinner Deal|Dart Game|
|---|---|---|
|Uncertain inputs|Weekly sales X and Y|Random coordinates X and Y|
|Probability model|Uniform and Normal|Uniform|
|Model logic|Ratio thresholds determine payer|Distance rule determines hit|
|Replication|200 simulated weeks|100–5,000 simulated darts|
|Primary output|Payment outcome distribution|p̂, π̂, confidence interval|
|Analytical insight|Rule can create asymmetric burden|Larger N improves precision|

The two cases also illustrate **two distinct uses of Monte Carlo
simulation**.

### Decision-Rule Evaluation

The Dinner Deal uses simulation to determine how an explicit policy
behaves when applied repeatedly under uncertain conditions.

### Statistical Estimation

The Dart Game uses simulation to estimate a probability and illustrates
how replication size affects the reliability of the estimate.

Both applications are relevant to business analytics: simulation can
help analysts understand the consequences of uncertain systems and
quantify the reliability of estimates used in decision making.

---

# Excel Techniques Demonstrated

The workbook demonstrates:

-   Monte Carlo simulation
-   `RAND()`
-   `NORM.INV()`
-   Uniform random-variable generation
-   Normal random-variable generation
-   `IF()`-based decision logic
-   Ratio-based decision rules
-   Repeated stochastic trials
-   Frequency analysis
-   Bernoulli indicators
-   Probability estimation
-   Sample standard deviation
-   Standard error
-   95% confidence intervals
-   Simulation convergence analysis
-   Sample-size comparison
-   Business-oriented interpretation of stochastic results

---

# Key Takeaways

**1. Decision rules should be evaluated across distributions.**\
The Dinner Deal demonstrates that threshold rules can interact with
heterogeneous stochastic inputs to create strongly uneven outcomes.

**2. A deterministic average can hide important behavior.**\
Simulation makes it possible to observe how frequently different
outcomes occur rather than evaluating only a single representative
scenario.

**3. Point estimates should be accompanied by uncertainty measures.**\
A Monte Carlo estimate without a confidence interval can imply more
precision than the simulation actually provides.

**4. Larger simulations generally improve precision, not necessarily
every realized point estimate.**\
The Dart Game shows that estimates can fluctuate non-monotonically even
while confidence intervals become systematically narrower.

**5. Simulation size involves a precision--computation trade-off.**\
Because standard error decreases approximately with `1/√N`,
progressively larger increases in simulation size are required to
achieve the same incremental improvement in precision.

**6. Simulation is most useful when treated as an analytical
experiment.**\
The value of Monte Carlo analysis comes from explicit assumptions,
transparent model logic, repeated trials, statistical output analysis,
and interpretation tied to a decision question.

---

# Model Limitations

### Dinner Deal

The results are conditional on the assumed sales distributions and
threshold values.

Mary's sales are modeled with a Normal distribution, which has unbounded
support and can theoretically generate nonpositive values. Because
Mary's sales also appear in the denominator of the performance ratio,
values close to zero can generate extreme ratios.

The model preserves this specification, but a real managerial
application should validate the assumed distribution against observed
data and consider a positive-support or truncated distribution where
appropriate.

The interpretation of fairness is also definition dependent. This
analysis uses the **frequency of paying for dinner** because that is the
outcome recorded by the model. Alternative fairness definitions could
incorporate dinner cost, income, sales performance, utility, or
negotiated preferences.

### Dart Game

Each sample size represents one random simulation realization rather
than repeated independent estimates of the entire Monte Carlo estimator.

The case therefore illustrates convergence and declining
confidence-interval width, but it does not empirically construct the
full sampling distribution of `π̂` at each sample size.

The geometric value of π is also known analytically, so this case serves
primarily as a controlled demonstration of Monte Carlo estimation and
simulation precision.

### Recalculation

The workbook uses volatile random-number functions. Recalculating the
spreadsheet generates new random realizations, so exact frequencies and
point estimates may change.

The numerical results reported here correspond to the saved workbook
snapshot and should be interpreted as one realization of the specified
stochastic models.

---

# Repository Files

``` text
├── 01_Monte_Carlo_Simulation_Portfolio_Project.xlsx
├── 01_Monte_Carlo_Portfolio_Report.pdf
└── README.md
```

### Excel Workbook

Contains the stochastic input generation, simulation logic, output
calculations, statistical summaries, visualizations, and interpretation
for both Monte Carlo applications.

### Portfolio Report

Provides a research-style discussion of the modeling framework,
simulation methodology, empirical results, statistical precision,
limitations, and business implications.

---

# Project Focus

**Business Analytics · Monte Carlo Simulation · Decision Analysis ·
Probability Modeling · Statistical Estimation · Simulation Convergence ·
Excel Modeling**

---

## Author

**Keman Xiang**

*PhD Application Portfolio*

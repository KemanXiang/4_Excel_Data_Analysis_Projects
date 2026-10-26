# Credit Rating Dynamics and Default Risk: A Markov Chain Simulation Study

**MGT239 — Simulation for Business | Research Portfolio Project**  
**Author:** Keman Xiang  
**Methods:** Discrete-time Markov chains · Monte Carlo simulation · Credit migration · Absorbing states · Stationary distributions · First-passage time  
**Tools:** Microsoft Excel

## Project Overview

Credit ratings evolve as firms remain in their current category, improve or deteriorate, or default. The long-run implications depend on whether the analysis follows a **fixed cohort of firms** or a **continuing sector in which defaulted positions are replaced**. This project uses a **three-state Markov chain** and **Excel-based Monte Carlo simulation** to examine both interpretations, compare simulated outcomes with analytical benchmarks, and assess implications for credit-risk monitoring and portfolio planning.

The transition probabilities are **illustrative model inputs**, not estimated from historical credit-rating agency data. The project is a methodological simulation study rather than a forecast of a specific real-world portfolio.

## Project Files

|File|Description|
|---|---|
|`10_Credit_Rating_Simulation_Portfolio.xlsx`|Complete Excel research portfolio, including original simulation calculations, linked analytical results, documentation, and visualizations.|
|`10_Credit_Rating_Dynamics_and_Default_Risk.pdf`|Companion research-style report with background, model, simulation design, results, interpretation, managerial implications, and limitations.|
|`README.md`|Project overview, model summary, selected findings, and reproduction guidance.|

## Research Questions

|Question|Analytical objective|
|---|---|
|(a)|Estimate year-2 and year-5 rating distributions for initially B-rated firms, and corresponding Default probabilities for initially A-rated firms.|
|(b)|Project a portfolio initially containing 300 A-rated and 700 B-rated firms at years 2, 5, 10, 50, and 200.|
|(c)|Explain the long-run consequences of an absorbing Default state.|
|(d)|Introduce a replacement mechanism for defaulted positions and specify its transition matrix.|
|(e)|Estimate the year-200 rating distribution, long-run A share, and annual default-event fraction under replacement.|
|(f)|Estimate the expected number of transitions until first Default for a firm initially rated A.|

## Model Specification

The three states are **A (1)**, **B (2)**, and **Default (3)**. The baseline annual transition matrix is:

```text
                 Next year
                A      B    Default
Current A      0.81   0.18    0.01
Current B      0.17   0.77    0.06
Current Default 0.00  0.00    1.00
```

In this **absorbing-default model**, a firm that defaults remains in Default. For the replacement specification, a defaulted position is occupied the following year by a new A-rated or B-rated firm, each with probability 0.5:

```text
                 Next year
                A      B    Default
Current A      0.81   0.18    0.01
Current B      0.17   0.77    0.06
Current Default 0.50  0.50    0.00
```

The replacement rule describes a **new firm occupying the position**, not recovery of the original defaulted company. With initial distribution `f1 = (0.30, 0.70, 0)`, the year-`t` analytical distribution is `f_t = f1 × P^(t−1)` because year 1 is the initial state.

## Simulation Design

- **Population:** 1,000 simulated rating paths.
- **Horizon:** 200 annual states per path.
- **Initial portfolio:** 30% A, 70% B, 0% Default.
- **Sampling:** Excel `RAND()` combined with cumulative transition probabilities and `MATCH`/`INDEX`.
- **Two specifications:** separate simulated paths for absorbing Default and firm replacement.
- **Validation:** comparison of simulated rating proportions with matrix-based analytical distributions and the replacement model's stationary distribution.
- **First-passage analysis:** identify the first Default on paths initially rated A, then express its position as elapsed transitions using the workbook's `MATCH − 1` convention and finite-horizon cutoff.

The workbook uses volatile random-number formulas. **Recalculating the file may change simulated outcomes**; the results below refer to the saved workbook snapshot documented in the companion report.

## Selected Results

### Conditional migration and absorbing-default portfolio

For a firm initially rated B, the **analytical** probability of Default is **6.00% in year 2** and **18.29% in year 5**. For a firm initially rated A, the corresponding analytical probabilities are **1.00%** and **7.94%**. The Excel workbook additionally reports sample-based conditional distributions and visualizes both initial-rating groups.

For the fixed-cohort absorbing model, the **saved year-200 simulation** is approximately **0.1% A, 0.1% B, and 99.8% Default**. This reflects accumulation in an absorbing state, not the disappearance of all firms from the real economy.

### Long-run composition under firm replacement

|Rating|Year-200 Monte Carlo share|Analytical stationary share|
|---|---:|---:|
|A|50.6%|50.24%|
|B|46.3%|46.47%|
|Default|3.1%|3.29%|

The replacement mechanism yields a stable *distribution of rated positions* rather than an absorbing portfolio. The stationary Default share is a stylized long-run fraction of positions registering a default event in a period; it is **not** a loss rate without additional exposure and loss-given-default assumptions.

### First-passage time from A

The saved workbook's conditional Monte Carlo estimate is **28.434 elapsed transitions** to first Default for paths initially rated A. The corresponding **infinite-horizon analytical benchmark** is approximately **31.298 transitions**. The finite 200-state simulation and its cutoff convention should be considered when interpreting this difference; the Monte Carlo estimate is not an exact analytical expectation.

## Visualizations and Interpretation

The workbook and report examine conditional migration, fixed-cohort portfolio evolution, replacement-model year-200 composition, and the **200-period convergence of replacement-model rating shares**. The convergence view helps distinguish:

1. **Transient dynamics:** rating shares initially reflect the starting mix.
2. **Long-run distribution:** the replacement model approaches stable proportions.
3. **Monte Carlo variation:** finite-sample shares fluctuate around analytical stationary levels even after convergence.

Convergence of aggregate shares does **not** mean individual firms stop migrating between ratings.

## Managerial and Analytical Implications

- **Horizon-sensitive credit monitoring:** single-year default probabilities understate the importance of multiyear migration pathways.
- **Cohort versus sector analysis:** tracking the fate of original firms and modeling an ongoing sector answer fundamentally different business questions.
- **Portfolio and capital planning:** stationary rating and default-event shares can inform scenario analysis, but expected losses require exposure and recovery assumptions.
- **Model validation:** analytical transition probabilities and stationary distributions provide benchmarks against which to assess stochastic simulations.

## Limitations

The model uses only three rating states and assumes time-homogeneous, firm-independent transitions. It omits macroeconomic regimes, correlated defaults, exposure sizes, recovery rates, and heterogeneous firm characteristics. The replacement process holds the number of modeled positions constant without modeling actual firm entry decisions. The finite simulation horizon also introduces a cutoff in first-passage estimation. Consequently, the results demonstrate **model behavior under specified assumptions**, not empirically calibrated real-world credit risk.

## How to Explore the Workbook

1. Open `10_Credit_Rating_Simulation_Portfolio.xlsx` in Microsoft Excel.
2. Start with the project guide and executive dashboard for the research narrative and headline results.
3. Review the framework, validation, interpretation, and documentation sheets for analytical assumptions and linked outputs.
4. Inspect `1.Credit_Rating` for transition matrices, conditional calculations, sample paths, and underlying statistics.
5. Read `10_Credit_Rating_Dynamics_and_Default_Risk.docx` for the full discussion of Questions (a)–(f), figures, theoretical comparisons, and limitations.

**Reproducibility note:** The workbook contains `RAND()`-based formulas. To preserve a particular simulation realization, retain the saved workbook snapshot before forcing recalculation. Do not interpret changes after recalculation as corrections to the model.

## References

- Kiefer, N. M., & Larson, C. E. (2007). A simulation estimator for testing the time homogeneity of credit rating transitions. *Journal of Empirical Finance, 14*(5), 818–835. https://doi.org/10.1016/j.jempfin.2006.08.001
- Lencastre, P., Raischel, F., Lind, P. G., & Rogers, T. (2014). Are credit ratings time-homogeneous and Markov? *arXiv:1403.8018*. https://arxiv.org/abs/1403.8018

---

*Keman Xiang PhD Application Portfolio*

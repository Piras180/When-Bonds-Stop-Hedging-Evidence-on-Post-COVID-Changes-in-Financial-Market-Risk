# When Bonds Stop Hedging

### Evidence on Post-COVID Changes in Financial Market Risk

**Financial econometrics · Multi-asset risk · Dynamic correlations · Portfolio construction**

An empirical research project completed for the **Empirical Methods in Finance** course at **HEC Lausanne (2026)**. The study examines whether financial market risk changed after COVID-19—not simply through higher volatility, but through shifts in **cross-asset correlations, tail behaviour, and diversification**.

**Research question:** *Has the structure of financial market risk changed since COVID-19?*

[**Explore the Python analysis**](./Notebook.ipynb) · [**Read the full research report**](./EMIF_Report%281%29.pdf)

## Project overview

The analysis uses **nine financial series** covering U.S., European and emerging-market equities; investment-grade and high-yield bonds; gold; oil futures; and U.S. and German government bond yields. The sample spans **January 2005–April 2026**.

To compare risk regimes, the study separates **2005–2019 (pre-COVID)** from **2021–2026 (post-COVID)**, treating 2020 as a transition year. Government-bond yield changes are converted into approximate returns using modified duration.

The objective is to answer three related questions:

1. Did volatility shocks become more persistent after COVID-19?
2. Did the stock–bond correlation, central to diversified portfolios, change materially?
3. What do changing correlations imply for traditional 60/40 and risk-based portfolio allocations?

## Methodology and Python implementation

| Area | Approach |
|---|---|
| Data preparation | Clean and align daily series; calculate log returns and duration-based bond-return proxies |
| Distribution and volatility diagnostics | Jarque–Bera, ARCH-LM, Ljung–Box, volatility clustering and rolling correlations |
| Conditional volatility | Compare ARCH/GARCH specifications with BIC; estimate Student-t GARCH models and volatility persistence |
| Dynamic dependence | Apply a **calibrated DCC-style correlation filter** to standardized GARCH residuals and construct time-varying covariance matrices |
| Statistical inference | Compare pre/post correlations; test candidate breaks in March 2020 and January 2022 using **Newey–West HAC** standard errors |
| Regime analysis | Fit a two-state Markov-switching model to weekly stock–government-bond correlations |
| Portfolio analysis | Evaluate a **60/40 stock–bond benchmark** and a monthly-rebalanced **Equal Risk Contribution (ERC)** portfolio |
| Robustness | Compare results with exponentially weighted moving average (EWMA) correlation estimates |

The notebook includes Python implementations of the volatility-estimation routines, DCC-style recursion, covariance construction, constrained ERC optimization, and portfolio-performance analysis. Figures and summary tables are exported automatically.

## Selected empirical findings

### 1. The traditional stock–bond hedge weakened

The average DCC-style correlation between the **S&P 500** and a **U.S. 10-year government-bond return proxy** moved substantially closer to zero:

| Average conditional correlation | Pre-COVID (2005–2019) | Post-COVID (2021–2026) |
|---|---:|---:|
| S&P 500 / U.S. 10Y government-bond proxy | **−0.325** | **−0.040** |
| S&P 500 / U.S. investment-grade bonds | −0.222 | +0.083 |

This suggests a weaker diversification benefit from fixed income during the later sample. Tests using the selected break dates show a larger estimated shift at **January 2022** than at **March 2020**, consistent with the importance of the inflation and monetary-tightening period.

### 2. Volatility persistence remained high, while tail risk mattered

Student-t GARCH estimates indicate persistent volatility and non-Gaussian return behaviour across the asset panel. The evidence does **not** point to a uniform increase in volatility persistence after COVID-19. Changes in how assets move together appear more important for the project's central risk-management question.

### 3. Portfolio implications depend on the allocation framework

| Performance measure | Pre-COVID | Post-COVID |
|---|---:|---:|
| 60/40 annualized volatility | 9.98% | 10.62% |
| 60/40 Sharpe ratio | 0.14 | 0.15 |
| ERC Sharpe ratio | **0.29** | **−0.25** |

The conventional **60/40 portfolio** exhibits only modest changes in these headline performance measures, despite weaker stock–bond hedging. The **ERC portfolio** shows a more pronounced deterioration in risk-adjusted performance in the post-COVID subsample.

**Main conclusion:** Asset allocation frameworks should account for **time-varying correlations and changing macroeconomic regimes**, rather than relying on historically stable stock–bond diversification.

## Technical skills demonstrated

- **Python:** NumPy, pandas, SciPy, Matplotlib, statsmodels, Jupyter Notebook
- **Financial econometrics:** ARCH/GARCH, Student-t likelihood, dynamic correlation filtering, Markov switching, structural-break regressions, HAC inference
- **Risk management:** Conditional covariance matrices, volatility clustering, tail behaviour, correlation regimes
- **Portfolio analytics:** Constrained optimization, equal risk contribution, rebalancing, Sharpe ratios, annualized volatility and drawdowns
- **Research practice:** Model comparison, robustness checks, economic interpretation, and discussion of limitations

## Repository files

```text
.
├── README.md               # Project overview and key findings
├── Notebook.ipynb          # Python analysis, figures and saved outputs
└── EMIF_Report(1).pdf      # Full research report
```

## Reproducing the analysis

The notebook contains saved outputs and can be **reviewed on GitHub without running it**. To reproduce the calculations, the original project dataset is required.

1. Install Python and Jupyter Notebook, together with the required dependencies:

   ```bash
   python -m pip install numpy pandas scipy matplotlib statsmodels openpyxl notebook
   ```

2. Place the input Excel workbook named **`Data.xlsx`** in the same directory as `Notebook.ipynb`. The notebook reads its first sheet and expects the original course-data column names.
3. Run `jupyter notebook`, open `Notebook.ipynb`, and execute the cells in order.

The notebook creates `Figures/` and `Tables/` to store charts and exported results. **`Data.xlsx` is not included** in the provided repository materials, so rerunning the notebook requires access to the original dataset.

## Scope and limitations

The results are **sample-specific**, not proof of a permanent structural regime change. The DCC-style coefficients are **calibrated**, not estimated jointly; government-bond returns are **duration-based approximations**; and the candidate break dates are chosen in advance. Portfolio comparisons use a simplified setup, and the ERC exercise omits transaction costs. The results should be interpreted as academic evidence about diversification and risk—not as a live investment strategy.

## Authors

**Matteo Piras · Marco D’Amico · Roberto Berardi**  
*Empirical Methods in Finance — HEC Lausanne, 2026*

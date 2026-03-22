# Portfolio Results

The system runs four independently validated ML models — one per instrument — combined into a single portfolio with conservative capital allocation. Each model is trained exclusively on historical data and tested on a forward period it has never seen.

## Combined Portfolio

| Metric | Value |
|--------|-------|
| Combined Sharpe Ratio | **3.74** |
| Deflated Sharpe Ratio (20 trials) | **1.000** |
| Maximum Drawdown | **-8.8%** |
| Capital deployed per trade | 5% per instrument |
| Total capital at risk | 20% |
| Cash allocation | 80% (earning risk-free rate) |

The portfolio allocates 5% of capital to each trade, across four instruments. At any given time, approximately 80% of the portfolio sits in cash. This conservative allocation limits drawdowns while the diversified signal generation maintains high risk-adjusted returns.

A Sharpe Ratio of 3.74 with only 20% of capital deployed means the strategy is capital-efficient — there is significant headroom to scale allocation if desired, at the cost of proportionally larger drawdowns.

???+ note "Calendar-Time vs Per-Trade Sharpe Ratios"
    The Sharpe Ratios on this page are **calendar-time** — calculated from daily portfolio returns including days with no active positions. This is the honest measurement: it reflects what an investor actually experiences. Per-trade Sharpe Ratios (calculated only across trade durations) are substantially higher, but they overstate real performance by ignoring idle periods.

## Per-Instrument Performance

Each instrument is independently modelled, trained, and validated. All four pass the most stringent statistical test at 20 trials.

| Instrument | Sharpe Ratio | DSR (n=20) | Trades | Test Period | Max Drawdown |
|------------|-------------|------------|--------|-------------|-------------|
| **SPY** (S&P 500) | 2.20 | 1.000 | 1,235 | 10 years | -6.7% |
| **TLT** (US 20Y+ Bonds) | 2.94 | 1.000 | 556 | 7 years | -2.7% |
| **GLD** (Gold) | 2.87 | 1.000 | 803 | 6.5 years | -3.1% |
| **QQQ** (Nasdaq 100) | 2.22 | 1.000 | 906 | 8 years | -3.9% |

3,500 total trades across all instruments, every one independently validated as statistically significant.

For context: buy-and-hold for each instrument over the same period produces DSR values of 0.000 (SPY), 0.000 (TLT), 0.017 (GLD), and 0.000 (QQQ). A DSR of zero means the observed buy-and-hold Sharpe Ratio is exactly what you'd expect from the best of 20 random strategies — statistically indistinguishable from luck.

## Diversification

The real power of the portfolio comes from combining signals with low correlations:

|  | SPY | TLT | GLD | QQQ |
|--|-----|-----|-----|-----|
| **SPY** | 1.00 | **-0.06** | 0.09 | 0.70 |
| **TLT** | **-0.06** | 1.00 | 0.10 | **0.00** |
| **GLD** | 0.09 | 0.10 | 1.00 | 0.11 |
| **QQQ** | 0.70 | **0.00** | 0.11 | 1.00 |

SPY and QQQ are correlated (0.70) — expected, since both are US equity indices. But bonds and gold provide genuine diversification:

- **TLT–SPY: -0.06** — slightly negative correlation, the classic equity-bond hedge
- **GLD–SPY: 0.09** — near-zero, independent signal source
- **TLT–QQQ: 0.00** — completely uncorrelated
- **TLT–GLD: 0.10** — near-zero

When equity models are wrong, the bond and gold models are not systematically wrong at the same time. This is not engineered — it's a natural consequence of training independent models on assets with different return drivers.

## Risk Profile

| Risk Metric | Value |
|-------------|-------|
| Maximum drawdown | -8.8% |
| Capital at risk | 20% of portfolio |
| Cash buffer | 80% |
| Worst single-instrument drawdown | -6.7% (SPY) |

The -8.8% maximum drawdown occurs across the entire out-of-sample period — including the COVID crash of 2020 and the 2022 bear market. For context, SPY itself fell approximately -34% during the COVID crash.

The 80% cash allocation acts as a structural buffer. Even in the worst case, the portfolio's maximum loss is bounded by the capital actually deployed.

---

## Research History

This portfolio is the product of iterative research, each stage independently validated:

1. **[S&P 500 Model](results.md)** — A single model established that an ML-driven edge exists in daily equity data, with SR 2.36 and DSR 0.955 over 10 years.
2. **[Strategy Refinement](strategy-evolution.md)** — Three labeling variants were tested to increase trade frequency while maintaining per-trade edge.
3. **Multi-Instrument Expansion** — The validated methodology was applied to bonds, gold, and Nasdaq 100, producing four independently robust models with natural diversification.

Each stage was validated before proceeding to the next. No results from later stages were used to inform earlier decisions.

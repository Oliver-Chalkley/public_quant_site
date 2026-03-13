# Strategy Evolution

The original model — documented in [Results](results.md) — established that a statistically robust edge exists in SPY daily data. Since then, I've explored three strategy variants to understand the nature of that edge and how far it can be pushed.

All three variants use the same data, feature engineering, and validation framework. They differ only in how training labels are constructed and which signals are executed at test time.

## Three Variants

| Variant | Labeling | Execution | Break-even Accuracy |
|---------|----------|-----------|---------------------|
| **A** (original) | Asymmetric boundaries | Long signals only | ~28% |
| **B** | Symmetric boundaries | Long and short signals | 50% |
| **C** | Symmetric boundaries | Long signals only | 50% |

## Performance (10-Year Out-of-Sample)

Same test period as the original results: 2016–2026, trained on pre-2016 data.

| Metric | Variant A | Variant B | Variant C |
|--------|-----------|-----------|-----------|
| Trades | 329 | 1,391 | **1,199** |
| Trades / year | 32 | 139 | **120** |
| Win rate | 52.6% | 61.9% | **63.8%** |
| EV per trade | +0.55% | +0.51% | **+0.60%** |
| Total return | +182% | +710% | **+724%** |

## Statistical Robustness

| Metric | Variant A | Variant B | Variant C |
|--------|-----------|-----------|-----------|
| Annualised Sharpe Ratio | 2.13 | 2.87 | **3.18** |
| DSR (n=5) | 0.999 | 1.000 | **1.000** |
| DSR (n=10) | 0.973 | 1.000 | **1.000** |
| DSR (n=20) | 0.783 | 0.999 | **1.000** |
| Verdict | Marginal | Pass | **Pass** |

Variant A's DSR dropped from 0.955 to 0.783 after retraining with two additional days of data — a sign that 329 trades over 10 years is not enough for stable statistical confidence. Variants B and C, with 4x the trade count, are immune to this instability.

## Year-by-Year (Variant C)

| Year | Trades | Win Rate | Return |
|------|--------|----------|--------|
| 2016 | 69 | 61% | +32.1% |
| 2017 | 133 | 69% | +50.7% |
| 2018 | 108 | 48% | -17.0% |
| 2019 | 133 | 71% | +107.6% |
| 2020 | 119 | 75% | +196.5% |
| 2021 | 119 | 60% | +47.2% |
| 2022 | 110 | 60% | +81.6% |
| 2023 | 146 | 64% | +75.1% |
| 2024 | 134 | 63% | +60.8% |
| 2025 | 111 | 70% | +105.5% |
| 2026 | 17 | 18% | -16.4% |

**9 of 11 years profitable.** The two negative years (2018 and partial 2026) have win rates below the 50% break-even — exactly when the strategy should lose money.

The regime adaptation observed in the [original model](results.md#emergent-regime-adaptation) is still present and more pronounced at higher trade frequency:

- **2020:** +196.5% — the model's best year, with 75% accuracy across 119 trades during the COVID recovery.
- **2022 (bear market):** +81.6% return with 60% accuracy. The model found profitable opportunities within the broader decline.
- **2018:** The one full losing year (-17.0%). A choppy, volatile market where accuracy dipped below break-even. The loss is contained and recoverable.

Trade frequency varies **2.1x** across years (69 to 146), compared to 3.5x in the original model — more consistent deployment of capital.

## Key Takeaways

Symmetric labeling eliminated a directional bias in the training data, allowing the model to generate substantially more trade signals without sacrificing per-trade expected value. The short signals in Variant B contributed zero edge — 50% win rate at 50% break-even — confirming that the strategy's value is concentrated on the long side.

Variant C is now the active production model.

| Metric | Original Model | Current Model |
|--------|----------------|---------------|
| Sharpe Ratio | 2.36 | **3.18** |
| DSR (n=20) | 0.955 | **1.000** |
| Trades / year | 32 | **120** |
| EV per trade | +0.63% | **+0.60%** |
| Total return (10yr) | +203% | **+724%** |

The per-trade expected value is comparable. The difference in total return comes from executing a similar edge four times as often.

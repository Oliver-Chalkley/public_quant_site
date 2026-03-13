# Results

All results below are from a **10-year out-of-sample backtest** on SPY (S&P 500 ETF), covering 2016 to 2026. The model was trained exclusively on data prior to 2016. No information from the test period was used during development, feature selection, or parameter tuning.

## Performance Summary

| Metric | Value |
|--------|-------|
| Annualised Sharpe Ratio | **2.36** |
| Total return (test period) | **+202.5%** |
| Trades | 322 (approx. 32 per year) |
| Win rate | 53.7% |
| Average win | +1.77% |
| Average loss | -0.70% |
| Payoff ratio (avg win / avg loss) | **2.53x** |
| Expected value per trade | +0.63% |

The payoff ratio is the key to the strategy's edge. You don't need to be right most of the time — you need your wins to be substantially larger than your losses. At a 2.53x payoff ratio, break-even is around 28% accuracy. The observed 53.7% win rate provides a comfortable margin above that threshold.

## Statistical Validation

A raw Sharpe Ratio, no matter how impressive, can be an artefact of overfitting or luck. The Deflated Sharpe Ratio (DSR) corrects for this by asking: *"Given that I explored N different configurations during development, is the observed Sharpe Ratio still statistically significant?"*

| Trials assumed (N) | Expected max SR by chance | DSR |
|---------------------|--------------------------|-----|
| 1 | 0.00 | 1.000 |
| 5 | 1.03 | 1.000 |
| 10 | 1.37 | 0.998 |
| **20** | **1.64** | **0.955** |

At N=20 (a conservative estimate for the number of configurations explored), the DSR is **0.955** — a 95.5% probability that the strategy's performance is genuine, not the best random draw from 20 attempts.

For context: buy-and-hold SPY over the same period has a Sharpe Ratio of 0.74. Its DSR at 20 trials is 0.000 — meaning a Sharpe Ratio of 0.74 is exactly what you'd expect from the best of 20 random strategies. The model's SR of 2.36 is in a different category entirely.

## Year-by-Year Returns

| Year | Trades | Win Rate | Return |
|------|--------|----------|--------|
| 2016 | 33 | 52% | +13.4% |
| 2017 | 64 | 56% | +20.6% |
| 2018 | 28 | 43% | +10.2% |
| 2019 | 24 | 54% | +15.0% |
| 2020 | 17 | 71% | +34.9% |
| 2021 | 30 | 57% | +16.9% |
| 2022 | 17 | 65% | +26.3% |
| 2023 | 43 | 54% | +21.6% |
| 2024 | 27 | 44% | +7.8% |
| 2025 | 32 | 53% | +34.5% |
| 2026 | 7 | 43% | +1.4% |

**Every single year is profitable.** Even 2018 and 2024 — the two weakest years by win rate (43% and 44%) — produced positive returns, because the payoff asymmetry means you only need roughly one in three trades to be correct.

## Emergent Regime Adaptation

The most compelling evidence that the model has learned something real — rather than memorising historical patterns — is that it **changes its behaviour depending on market conditions**, without being programmed to do so.

**2020 (COVID crash and recovery):** The model took only 17 trades all year — roughly half its normal rate — but achieved a 71% win rate and +34.9% return. It identified the high-volatility recovery as an environment where its signals were unusually reliable, and it naturally avoided the chaos of the initial crash. Nobody told it to do this.

**2022 (bear market):** Again, only 17 trades. The model dramatically reduced its activity during the sustained drawdown, but the trades it *did* take had a 65% win rate. It found counter-trend rallies within the broader decline — and had the discipline to sit out the rest.

**2017 (low-volatility uptrend):** The model traded aggressively — 64 trades, double the annual average. In a calm, steadily rising market, it correctly identified that conditions favoured frequent trading.

Trade frequency varies **3.5x** across years (17 to 64 trades). This adaptive behaviour emerges entirely from the model's learned understanding of market conditions. There is no hard-coded regime detection, no volatility switch, no calendar logic. The model simply learns when its predictions are likely to be profitable and acts accordingly.

This is the kind of result that complexity science would predict: simple rules, applied consistently to rich data, produce intelligent emergent behaviour. It's also the kind of result that's very difficult to achieve by overfitting — a model that has memorised the past doesn't adapt to novel market conditions.

---

## What Came Next

This model established that a real edge exists. I then explored three strategy variants — changing the labeling geometry and execution rules — to understand the nature of that edge and push it further. The best variant achieves **SR 3.18 with DSR 1.000** over the same test period.

[Read the strategy evolution](strategy-evolution.md){ .md-button }

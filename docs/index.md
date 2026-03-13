# Systematic, Statistically-Validated Equity Strategies

Most quantitative backtests are broken. Parameters are tuned until the past looks good, then the strategy falls apart in live markets. The core problem isn't bad strategies — it's bad evaluation. If you can't distinguish skill from luck, you're gambling.

I build ML-driven trading models with one guiding principle: **prove it isn't luck before you trade it.**

---

## Headline Numbers

These results are from a 10-year out-of-sample backtest on SPY (S&P 500 ETF). The model was trained on data prior to 2016 and tested on 2016–2026 — a period it had never seen during development.

| Metric | Value |
|--------|-------|
| Annualised Sharpe Ratio | **2.36** |
| Deflated Sharpe Ratio (20 trials) | **0.955** |
| Years profitable | **10 out of 10** |
| Total trades | 322 |
| Win rate | 53.7% |
| Payoff ratio (avg win / avg loss) | 2.53x |
| Total return (test period) | +202.5% |

The Deflated Sharpe Ratio is the number that matters most. It answers: *"If I had tried 20 different strategies and picked the best one, would this result still be statistically significant?"* At 0.955, the answer is yes — there is a 95.5% probability this performance is real, not an artefact of overfitting.

[Read more about the results](results.md){ .md-button }
[Understand the approach](approach.md){ .md-button .md-button--primary }

---

## What's Next

I am now transitioning these validated models into live quantitative trading algorithms. The roadmap:

- **S&P 500 model** — first live strategy, launching soon (long-only)
- **Major indices** — FTSE 100, EURO STOXX 50, Nikkei 225 to follow
- **Individual equities** — expanding to single-stock models after index coverage
- **Long/short strategies** — extending beyond long-only once the live infrastructure is proven

The research and statistical validation are done. The engineering is underway.

---

## Latest: Strategy Evolution

Since the original model, I've explored three strategy variants — refining the labeling approach to increase trade frequency while maintaining per-trade edge. The result: **SR 3.18, DSR 1.000, +724% over 10 years.**

[Read the full comparison](strategy-evolution.md){ .md-button }

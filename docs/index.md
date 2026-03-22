# Systematic, Statistically-Validated Multi-Instrument Portfolio

Most quantitative backtests are broken. Parameters are tuned until the past looks good, then the strategy falls apart in live markets. The core problem isn't bad strategies — it's bad evaluation. If you can't distinguish skill from luck, you're gambling.

I build ML-driven trading models with one guiding principle: **prove it isn't luck before you trade it.**

---

## Portfolio at a Glance

Four independently validated models — spanning equities, bonds, and gold — combined into a single portfolio with natural diversification and conservative capital allocation.

| Metric | Value |
|--------|-------|
| Instruments | **SPY, TLT, GLD, QQQ** |
| Combined Sharpe Ratio | **3.74** |
| Deflated Sharpe Ratio (20 trials) | **1.000** |
| Maximum Drawdown | **-8.8%** |
| Capital deployed | 20% (80% in cash) |
| Total trades (all instruments) | 3,500+ |
| Out-of-sample test period | Up to 10 years |

Every instrument passes the Deflated Sharpe Ratio test independently — a 100% probability at 20 trials that the observed performance is real, not an artefact of overfitting. The combined portfolio benefits further from low cross-instrument correlations.

[View the full portfolio results](portfolio.md){ .md-button }
[Understand the approach](approach.md){ .md-button .md-button--primary }

---

## Evolution

This work began with a single model on S&P 500 data that [established a statistically robust edge](results.md) over a 10-year out-of-sample test. Subsequent research [refined the labeling methodology](strategy-evolution.md) to increase trade frequency while maintaining per-trade edge.

The current system extends that validated approach across four uncorrelated instruments — S&P 500, US Treasury bonds, gold, and Nasdaq 100 — creating a portfolio with natural diversification and strict risk controls. Each instrument model is independently trained and validated to the same standard.

---

## What's Next

The models are validated. The infrastructure is built. The transition to live trading is underway.

- **Multi-instrument portfolio** — four models validated and deployed
- **Live execution** — automated signal generation and order placement
- **International diversification** — additional markets and asset classes to follow
- **Continuous validation** — live performance monitored against backtest expectations

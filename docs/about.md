# About

## Background

I hold a PhD in mathematics, with a focus on complexity science — the study of systems where simple rules produce emergent, unpredictable behaviour. Financial markets are a canonical example: millions of agents acting on local information produce global dynamics that no single participant fully understands.

My professional career is in the testing and evaluation of AI systems. I assess how machine learning models behave under stress, where they fail, how they overfit, and whether their apparent performance is genuine or illusory. Very few people spend their working lives understanding how AI actually thinks — its strengths, its weaknesses, and the subtle ways it can mislead you into believing it works when it doesn't. I do this every day.

I also bring a broader set of experiences that shape how I think about risk and decision-making. I have a background in computer science and finance, years of serious poker — a game that is fundamentally about expected value under uncertainty — and I'm a lifelong Linux builder. I like to understand systems from the ground up, and I'd rather build the tools myself than trust a black box I can't inspect.

## Why This Matters for Trading

Quantitative trading is, at its core, a machine learning problem wrapped in a statistics problem. You need ML to find patterns in high-dimensional, non-linear market data. But you also need rigorous statistical evaluation to determine whether those patterns are real or just noise that happens to look good in a backtest.

Most quant practitioners have one of these skills. Very few have both. My background sits at the intersection:

- **Complexity science** gives me the right mental model for markets — they are adaptive systems, not stationary processes. Any strategy that assumes stable statistical properties will eventually fail.
- **AI evaluation** gives me the tools to catch overfitting before it costs money. I know exactly how a model can appear to perform well while learning nothing of value — because I test for this professionally.
- **Mathematics** provides the statistical framework to quantify uncertainty, correct for multiple testing, and make honest claims about expected performance.

## Philosophy

I do not believe in black-box trading. I believe in:

1. **Minimising false positives.** The most important property of a trading system is not how much money it makes in a backtest — it's how confident you can be that the backtest reflects reality. A strategy with a modest Sharpe Ratio and high statistical confidence will outperform a strategy with a spectacular Sharpe Ratio and no validation, because the second strategy is almost certainly overfit.

2. **Transforming data for ML.** Raw market data is poorly suited for machine learning. Prices are non-stationary, returns cluster in time, and standard labeling methods (e.g., "did the price go up over the next N days?") create noisy, misleading targets. The first and most important step is transforming the data into a form where ML algorithms can actually learn meaningful patterns rather than memorising noise.

3. **Letting the model surprise you.** The best test of a quantitative strategy is when it does something you didn't program it to do — and that something turns out to be correct. When my models naturally reduce trading during bear markets and increase trading during low-volatility uptrends, without any explicit regime-detection logic, that's evidence of genuine learned intelligence, not curve-fitting.

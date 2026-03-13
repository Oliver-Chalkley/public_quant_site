# Approach

## The Problem: Why Most Backtests Fail

The quant industry has a dirty secret: the vast majority of backtested strategies do not survive contact with live markets. This is not because the strategies are inherently bad — it's because the evaluation process itself is structurally flawed.

The most common failure modes:

**Overfitting.** You tune parameters until the backtest looks great. But the model has learned the noise in historical data, not the signal. Out of sample, it reverts to random.

**Look-ahead bias.** Information that would only be available in hindsight leaks into the training process. The model appears prescient in testing because it secretly had access to the future.

**Multiple testing.** You try 100 parameter combinations and report the best result. Statistically, at least a few of those will look excellent by pure chance. The reported Sharpe Ratio is inflated — sometimes dramatically.

**Naive labeling.** Labeling a trade as "profitable" because the price was higher N days later ignores what the price did during the holding period. A trade that was down 15% before recovering to +1% is not the same as a smooth 1% gain, but naive labeling treats them identically.

These are not bugs in implementation. They are structural flaws in the standard workflow. Fixing them requires a fundamentally different methodology.

## The Tooling Problem

Most retail trading platforms offer built-in backtesting — drag and drop some indicators, hit "run," and get a nice equity curve. The problem is that these tools make it almost impossible to evaluate a strategy honestly. They typically offer no protection against look-ahead bias, no correction for multiple testing, no way to implement proper time-series cross-validation, and no mechanism for statistical validation beyond raw returns.

The result is that retail traders are systematically misled by their own tools. A platform that reports a 200% backtest return with no Deflated Sharpe Ratio, no purged cross-validation, and no out-of-sample separation is not telling you whether the strategy works — it's telling you how well it memorised the past.

I don't use retail trading software. My entire pipeline runs on Linux servers I build and maintain myself — from data ingestion and feature engineering through model training, statistical validation, and signal execution. Every component is purpose-built for rigorous evaluation, not convenience. This is slower to set up but it means I control every assumption, every data split, and every statistical test. Nothing is hidden inside a platform I can't inspect.

## The Solution: Rigorous ML on Transformed Data

My approach addresses each of these failure modes systematically.

### 1. Data Transformation

Raw price data is non-stationary — its statistical properties change over time. Feeding it directly into a machine learning model is like trying to learn a language from a book where the grammar changes every chapter. The model memorises phrases instead of learning structure.

The first step is transforming market data into inputs with stable statistical properties. This involves encoding price, volume, and volatility information in ways that are comparable across different market regimes. The goal is not to predict the future from the past, but to describe the present in a form that ML algorithms can reason about.

### 2. Information-Theoretic Labeling

Instead of the standard approach of labeling trades based on fixed-horizon returns ("was the price higher 10 days later?"), I use a labeling method grounded in information theory. Each trade is evaluated against dynamic boundaries that adapt to current market volatility. This produces cleaner, more informative training labels — the model learns from well-defined outcomes rather than noisy price snapshots.

### 3. Multi-Model Architecture

Rather than relying on a single model to make all decisions at once, the pipeline uses multiple models that each handle a different aspect of the trading decision. This decomposition prevents the overfitting trap that comes from asking one model to do too many things — and it allows each model to be validated independently.

### 4. Leakage-Proof Validation

Standard cross-validation (randomly splitting data into train and test sets) is catastrophically wrong for time-series data. Adjacent data points share information — if Tuesday is in the training set and Wednesday is in the test set, the model has effectively seen the future.

I use cross-validation specifically designed for temporal data. Training and test sets are separated by buffer zones that prevent any information leakage. Every performance metric reported is from data the model genuinely could not have seen during training.

### 5. The Final Gate: Deflated Sharpe Ratio

Even with all the above precautions, there remains the multiple testing problem. During the development process, I explored different feature sets, model configurations, and parameter ranges. The best result from this exploration is biased upward — simply because I picked the best of several attempts.

The Deflated Sharpe Ratio (DSR) corrects for this directly. It asks: *"Given the number of configurations I explored, what is the probability that the observed performance is real rather than the expected best result from random strategies?"*

This is the final validation gate. A model that passes the DSR test has survived the most stringent statistical challenge I can throw at it. A model that fails is discarded, regardless of how impressive the raw backtest looks.

## The AI Angle

Markets are complex adaptive systems. The patterns that drive returns are non-linear, regime-dependent, and embedded in high-dimensional interactions between price, volume, volatility, and momentum. This is precisely the kind of problem where machine learning excels — *if* you set up the problem correctly.

The "if" is doing all the work in that sentence. Most applications of ML to trading fail not because ML is wrong for the job, but because the data pipeline, labeling, and evaluation are naive. The model dutifully learns whatever patterns are in the training data — including the spurious ones.

My background in AI testing and evaluation is specifically about catching this failure mode. I know how models overfit, how they exploit data leakage, and how they produce confident predictions from noise. Applying that same scepticism to my own trading models is what separates this approach from the standard backtest-and-hope workflow.

## Academic Foundations

This work builds on decades of research in quantitative finance, statistical learning, and econometrics. Key influences include:

- **Marcos López de Prado** — pioneering work on applying modern machine learning to finance with proper statistical rigour
- **David Bailey & Marcos López de Prado** — the Deflated Sharpe Ratio framework for correcting selection bias in backtesting
- **J.D. Opdyke** — asymptotic distribution theory for the Sharpe Ratio under non-normal returns
- **Robert Engle** — foundational work on modelling time-varying volatility in financial returns (Nobel Prize, 2003)
- **The broader complexity science literature** — understanding markets as adaptive systems rather than stationary processes

I stand on the shoulders of these researchers. My contribution is in the integration: combining these ideas into a coherent, end-to-end pipeline that transforms raw market data into statistically-validated trading decisions.

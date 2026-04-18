# Epsilon: Intraday Equity Trading Strategy

## Overview

A quantitative intraday trading strategy applied to NIFTY 100 equities, combining momentum, trend-following, and volatility-based risk management. The system is designed with realistic execution assumptions and avoids lookahead bias through strict use of lagged features.

---

## Strategy Pipeline

The strategy follows a structured multi-stage pipeline:

1. **Universe Construction**

   * NIFTY 100 stocks with 15-minute OHLCV data

2. **Daily Stock Selection**

   * Momentum filter: 20-day returns ≥ 1.5%
   * Trend filter: SMA(50) alignment
   * Trend strength: ADX(14) ≥ 18
   * Liquidity constraint: Avg volume > 500K
   * Volatility filter: 20-day std ≤ 18%

3. **Intraday Feature Engineering**

   * VWAP (volume-weighted price)
   * EMA(21) for short-term trend
   * ATR(14) for volatility
   * Opening Range (09:15–09:45)

4. **Signal Generation**

   * Breakout above/below opening range
   * Trend confirmation using VWAP + EMA
   * Volume surge filter (≥ 1.1× recent average)

5. **Execution Engine**

   * Trades executed at next bar open
   * Maximum 4 trades per symbol per day
   * Minimum spacing between trades to avoid clustering

6. **Risk Management**

   * Fixed fractional risk: 1% per trade
   * ATR-based stop-loss and trailing stop
   * End-of-day square-off (no overnight exposure)

---

## Backtesting Methodology

* Uses historical intraday data (15-minute resolution)
* Daily re-selection of stock universe
* Strict lagging of all indicators to eliminate lookahead bias
* Trades executed on next bar after signal generation
* Dynamic position sizing based on volatility
* Full trade-level logging for evaluation

### Assumptions

* No transaction costs or slippage
* No overnight positions
* Perfect liquidity at execution prices

---

## Performance

* Initial Capital: ₹100,000
* Final Capital: ₹127,971
* Cumulative Return: 27.97%
* Annualized Return: 28.22%
* Sharpe Ratio: 1.20
* Sortino Ratio: 2.17
* Max Drawdown: -19.00%
* Total Trades: 1248
* Average PnL per Trade: ₹21.82
* Win Rate: 49.28%

---

## Performance Insights

* Profitability is driven by **trend-following and breakout dynamics**
* Win rate below 50% highlights reliance on **risk-reward asymmetry**
* Sharpe ratio > 1 indicates consistent risk-adjusted returns
* Moderate drawdown (~19%) reflects controlled downside risk
* High trade count (~1200) improves statistical reliability

---

## Key Parameters

| Parameter             | Value | Description        |
| --------------------- | ----- | ------------------ |
| LOOKBACK              | 20    | Momentum window    |
| SMA_PERIOD            | 50    | Trend filter       |
| ADX_THRESHOLD         | 18    | Trend strength     |
| ATR_WINDOW            | 14    | Volatility measure |
| MAX_TRADES_PER_SYMBOL | 4     | Trade cap          |
| BASE_RISK_PER_TRADE   | 1%    | Risk per trade     |

---

## Repository Structure

* `strategy.ipynb` → full implementation
* `report.pdf` → detailed explanation

---

## Design Decisions

* **Opening Range Breakout (ORB):** captures early intraday momentum
* **VWAP + EMA confirmation:** filters false breakouts
* **ATR-based stops:** adapt to volatility
* **Lagged indicators:** ensure realistic backtesting
* **Trade spacing constraints:** reduce overtrading

---

## Limitations

* Does not include transaction costs or slippage
* Assumes perfect liquidity
* Performance may vary across market regimes
* Parameter sensitivity not explored

---

## Future Work

* Incorporate transaction cost and slippage modeling
* Perform parameter sensitivity analysis
* Extend to portfolio-level allocation
* Explore machine learning-based enhancements

---

## Reproducibility

* Entire strategy implemented in a single notebook
* Dataset is programmatically loaded and processed
* All results are reproducible from the provided code

---

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook strategy.ipynb
```

# Epsilon: Intraday Equity Trading Strategy

## Overview
A quantitative intraday trading strategy applied to NIFTY 100 equities, combining momentum, trend-following, and volatility-based risk management. The system is designed with realistic execution assumptions and no lookahead bias.

---

## Strategy Architecture

### 1. Stock Selection (Daily)
- Momentum filter: 20-day returns ≥ 1.5%
- Trend filter: SMA(50) alignment
- Trend strength: ADX(14) ≥ 18
- Liquidity constraint: Avg volume > 500K
- Volatility filter: 20-day std ≤ 18%

### 2. Signal Generation (Intraday)
- Opening Range Breakout (09:15–09:45)
- VWAP + EMA(21) trend confirmation
- Volume surge filter (≥ 1.1× recent average)

### 3. Execution Logic
- Trades executed at next bar open (prevents lookahead bias)
- Maximum 4 trades per symbol per day
- 15-minute timeframe

### 4. Risk Management
- Fixed fractional risk: 1% per trade
- ATR-based stop-loss and trailing stop
- End-of-day square-off (no overnight exposure)

---

## Performance

- Initial Capital: ₹100,000  
- Final Capital: ₹127,971  
- Cumulative Return: 27.97%  
- Annualized Return: 28.22%  
- Sharpe Ratio: 1.20  
- Sortino Ratio: 2.17  
- Max Drawdown: -19.00%  
- Total Trades: 1248  
- Avg PnL per Trade: ₹21.82  
- Win Rate: 49.28%

---

## Interpretation

- Profitability driven by **risk-reward asymmetry**, not win rate
- Sharpe > 1 indicates consistent risk-adjusted returns
- Moderate drawdown (~19%) reflects controlled downside risk
- High trade count (1200+) improves statistical reliability

---

## Key Features

- Multi-factor stock selection pipeline
- Intraday breakout strategy with confirmation filters
- Volatility-adjusted position sizing
- Fully backtested with realistic execution constraints
- No lookahead bias (strict lagged features)

---

## Repository Structure

```
notebooks/   → research & experimentation  
report/      → strategy documentation  
```

---

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook notebooks/strategy.ipynb
```

---

## Notes

- Strategy is designed for research purposes
- Does not include transaction costs or slippage (future work)

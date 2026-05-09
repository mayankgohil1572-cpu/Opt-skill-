# OPTS-SKILL — Smart Options Trading Strategy

> A quantitative options trading algorithm built on the principles of Steve Burns, Mark Douglas, and Jim Simons — applied to Indian F&O markets (SENSEX & NIFTY).

[![Pine Script](https://img.shields.io/badge/Pine%20Script-v5-blue)](https://www.tradingview.com)
[![Platform](https://img.shields.io/badge/Platform-TradingView-orange)](https://www.tradingview.com)
[![Market](https://img.shields.io/badge/Market-NSE%20%7C%20BSE-green)](https://www.nseindia.com)
[![Status](https://img.shields.io/badge/Status-Live%20Tested-brightgreen)](https://github.com)

-----

## 📈 Live Performance

|Period           |Starting Capital|Ending Capital|Return   |
|-----------------|----------------|--------------|---------|
|May 2026 (4 days)|₹5,000          |₹17,382       |**+247%**|


> Trades executed on Groww F&O using SENSEX weekly expiry options (Tuesday)

-----

## 🧠 Built On Three Frameworks

|Book                           |Author      |Principle Applied                                                                      |
|-------------------------------|------------|---------------------------------------------------------------------------------------|
|*New Trader Rich Trader*       |Steve Burns |2% risk rule, ATR stop loss, 1:1.5 R:R minimum                                         |
|*Trading in the Zone*          |Mark Douglas|Session filter, no-hesitation alerts, confluence requirement                           |
|*The Man Who Solved the Market*|Jim Simons  |ATR% volatility quantification, BB squeeze pattern detection, volume surge confirmation|

### Quant Finance Layer (Paul Wilmott)

- Put-Call Parity: `C - P = S - K·e^(-rT)` applied to live option chains
- 1 Standard Deviation move = `S × σ × √T` for strike selection
- Black-Scholes intuition for ATM vs OTM entry decisions

-----

## 🔧 How It Works

### Signal Types

|Signal            |Trigger                                                         |Action                             |
|------------------|----------------------------------------------------------------|-----------------------------------|
|🟢 **BUY CALL**    |EMA 9 > 21 > 50, RSI 50-70, Volume surge, Low ATR%, MACD bullish|Buy ATM Call, 30-45 DTE, 0.40 Delta|
|🔴 **BUY PUT**     |EMA 9 < 21 < 50, RSI 30-50, Volume surge, Low ATR%, MACD bearish|Buy ATM Put, 30-45 DTE, 0.40 Delta |
|⚡ **SELL PREMIUM**|High ATR%, RSI extreme, Trend established                       |Sell OTM Call/Put, collect premium |
|🔄 **STRADDLE**    |Bollinger Band squeeze detected                                 |Buy both Call + Put before big move|

### EMA System

```
EMA 9  (Cyan)   — Fast trend
EMA 21 (Orange) — Medium trend  
EMA 50 (Grey)   — Macro trend
```

**Bull signal:** All three aligned upward with price above all EMAs  
**Bear signal:** All three aligned downward with price below all EMAs

### Risk Management (Burns Rules — hardcoded)

```
Stop Loss    = Entry - (ATR × 2.0)     ← Set BEFORE entry
Take Profit  = Entry + (ATR × 3.0)     ← Minimum 1:1.5 R:R
Max Risk     = 2% of total capital      ← Never exceeded
```

-----

## ⚙️ Setup Instructions

### Step 1 — Add to TradingView

1. Open TradingView → your SENSEX or NIFTY chart
1. Click **Pine Editor** at the bottom
1. Delete default code
1. Paste contents of `OPTS-SKILL.pine`
1. Click **“Add to chart”**

### Step 2 — Recommended Settings

```
Chart:     5-minute candles
Index:     BSE:SENSEX or NSE:NIFTY
Session:   09:30–16:00 IST (auto-filtered)
Expiry:    SENSEX Tuesday / NIFTY Thursday
```

### Step 3 — Set Alerts

1. Right-click chart → **Add Alert**
1. Condition: **OPTS-SKILL**
1. Select signal type (CALL / PUT / STRADDLE)
1. Enable **Webhook URL** for automation (n8n → Gmail)

### Step 4 — Automation (Optional)

Connect to n8n webhook for real-time email/SMS alerts:

```
TradingView Webhook → n8n → Gmail Alert
```

-----

## 📊 Parameters Reference

|Parameter     |Default    |Description           |
|--------------|-----------|----------------------|
|Fast EMA      |9          |Short-term trend      |
|Slow EMA      |21         |Medium-term trend     |
|Trend EMA     |50         |Long-term trend filter|
|RSI Length    |14         |Momentum oscillator   |
|ATR Length    |14         |Volatility measurement|
|ATR Multiplier|1.5        |High vol threshold    |
|Volume MA     |20         |Volume baseline       |
|Volume Surge  |1.5×       |Confirmation threshold|
|Stop Loss     |2× ATR     |Risk management       |
|Take Profit   |3× ATR     |Reward target         |
|Session       |09:30-16:00|Indian market hours   |

-----

## 📋 Trading Rules

These rules are non-negotiable and apply to every trade:

1. **Never trade without OPTS-SKILL signal**
1. **Maximum 20% capital per trade** (1 lot SENSEX at current capital)
1. **Set stop loss BEFORE entry** — no exceptions
1. **Book 50% at Target 1** — lock profit, ride rest
1. **Hard exit 8:00 AM UK (1:30 PM IST)** on expiry day
1. **3 consecutive losses = 3-day mandatory break**
1. **Withdraw 20% every time capital doubles**

-----

## 🗂️ Repository Structure

```
opts-skill/
├── OPTS-SKILL.pine        ← Main strategy file (paste into TradingView)
├── README.md              ← This file
├── docs/
│   ├── SIGNALS.md         ← Detailed signal documentation
│   ├── RISK_MANAGEMENT.md ← Burns rules applied
│   └── WILMOTT_NOTES.md   ← Quant finance backing
└── backtest/
    └── results.md         ← Live trade results
```

-----

## 📚 Knowledge Foundation

This algorithm is the practical implementation of:

- **Paul Wilmott** — *Introduces Quantitative Finance* (Chapters 1-2)
- **Steve Burns** — *New Trader Rich Trader*
- **Mark Douglas** — *Trading in the Zone*
- **Jim Simons** — *The Man Who Solved the Market*
- **Maxwell Maltz** — *Psycho-Cybernetics* (discipline framework)

-----

## ⚠️ Disclaimer

This is an **educational project** documenting a personal trading system. Not financial advice. Past performance does not guarantee future results. Options trading involves substantial risk of loss.

-----

## 👤 Author

Built by a quantitative finance student applying Wilmott’s mathematical framework to live Indian F&O markets.

- 📊 Live trading on NSE/BSE since May 2026
- 📚 Studying: *Paul Wilmott Introduces Quantitative Finance*
- 🔧 Tools: Pine Script v5, TradingView, n8n automation, Python

-----

*“The consistency you seek is in your mind, not in the markets.” — Mark Douglas*

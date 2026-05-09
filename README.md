# Wilmott Quant Finance Applied to OPTS-SKILL

## Chapter 1 — No Arbitrage Pricing

### Forward Price

```
F = S × e^(rT)
```

Used to check if NIFTY/SENSEX futures are fairly priced vs spot.

### Log Returns

```
r = ln(S1/S0)
```

Used to calculate actual trade returns mathematically.

## Chapter 2 — Options Pricing

### Put-Call Parity (live check before every trade)

```
C - P = S - K × e^(-rT)
```

**Live example (09 May 2026):**

- S = 24,233, K = 24,200, r = 0.065, T = 4/365
- Theory: C - P = 24,233 - 24,183 = +50
- Actual: 189.60 - 138.70 = +50.90
- Mispricing: ₹0.90 (near fair — clean entry)

### 1 Standard Deviation Move (strike selection)

```
1 SD = S × σ × √T
     = 24,236 × 0.16 × √(4/365)
     = ±406 points
```

Buying zone for CALL: S - 1SD = 23,830
Buying zone for PUT:  S + 1SD = 24,642

### Black-Scholes Intuition

- ATM options: highest Delta (~0.50), best directional bet
- OTM options: cheaper but lower probability
- Theta decay fastest for ATM on expiry day

# Bitcoin Market Analysis & Quantitative Strategy Evaluation

## Overview

This project analyzes the historical behavior of Bitcoin (BTC-USD) and evaluates whether simple systematic trading rules can improve risk management compared to a passive buy-and-hold investment approach.

The goal is not to create a trading bot, but to study how quantitative methods can be used to understand volatility, trend behavior and drawdown control in highly volatile assets.

---

## Research Questions

* How volatile is Bitcoin on a daily basis?
* Does Bitcoin behave independently from traditional markets?
* Can trend-following rules reduce exposure during bear markets?
* Can risk management techniques reduce drawdowns without eliminating upside?

---

## Data Source

Historical daily price data was obtained using the **Yahoo Finance API (yfinance)**.

Assets analyzed:

* Bitcoin (BTC-USD)
* S&P 500 index (market reference)

The dataset is downloaded programmatically, ensuring reproducibility.

---

## Methodology

### 1. Exploratory Data Analysis

* Daily returns calculation
* Volatility visualization
* Distribution of returns
* Comparison with S&P500 behavior

### 2. Trend-Following Strategy

Implementation of moving-average crossover strategies using multiple window combinations to identify market regimes (bull vs bear periods).

Signals:

* Long when short moving average crosses above long moving average
* Exit when crossover reverses

### 3. Backtesting

* Strategy equity curve calculation
* Comparison with buy-and-hold performance
* Log-scale cumulative return analysis
* Multiple parameter combinations tested

### 4. Risk Management

Implementation and evaluation of:

* Trailing Stop-Loss
* Exposure reduction during downtrends
* Drawdown mitigation

---

## Results

### Daily Returns Distribution

![Daily Returns](https://private-us-east-1.manuscdn.com/sessionFile/XAgjA8hTTgQDFgsMXw39G3/sandbox/f6DBgFUKjRxo8Kx4CX1iId-images_1770764666236_na1fn_L2hvbWUvdWJ1bnR1L2JpdGNvaW5fcG9ydGZvbGlvX2VsaXRlL2ZpZ3VyZXMvMDFfZGFpbHlfcmV0dXJucw.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvWEFnakE4aFRUZ1FERmdzTVh3MzlHMy9zYW5kYm94L2Y2REJnRlVLalJ4bzhLeDRDWDFpSWQtaW1hZ2VzXzE3NzA3NjQ2NjYyMzZfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwySnBkR052YVc1ZmNHOXlkR1p2YkdsdlgyVnNhWFJsTDJacFozVnlaWE12TURGZlpHRnBiSGxmY21WMGRYSnVjdy5wbmciLCJDb25kaXRpb24iOnsiRGF0ZUxlc3NUaGFuIjp7IkFXUzpFcG9jaFRpbWUiOjE3OTg3NjE2MDB9fX1dfQ__&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=RLR~s53CblfIo7MzID4JtVQE7sPq6VP8PcP2snb0E5Egqbx7Uibyt2T~IMLChlOvJqqPCSt0mdmQkJNkLejkYW7VCNREMjkqwk8DvbwdutmMSv4F7BnPmy5JHeeptTnTBWvGEUip2IEQbJRwO1GTWg7pFDiYJb4ozThFDb4HaaggEM~hZ-yLdgnyjhUUoT6LMRJmUScSwMsk5Fb04yFRs5cw2zTtsakYzvTirojT5N57mCQb5vfP8SOz9Gs4-vIjAynC66tpLcP~bTw7QcL12a8d8QqnY~D0WOsy9pWaOqjzKGuri7LfnUDdLCsYwekDFSDiuUyd8rJCdmEyjZgLew__)

Bitcoin shows extremely high volatility with frequent large positive and negative daily returns.

### Trend Identification (Moving Averages)

![Moving Averages](https://private-us-east-1.manuscdn.com/sessionFile/XAgjA8hTTgQDFgsMXw39G3/sandbox/f6DBgFUKjRxo8Kx4CX1iId-images_1770764666236_na1fn_L2hvbWUvdWJ1bnR1L2JpdGNvaW5fcG9ydGZvbGlvX2VsaXRlL2ZpZ3VyZXMvMDJfbW92aW5nX2F2ZXJhZ2Vz.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvWEFnakE4aFRUZ1FERmdzTVh3MzlHMy9zYW5kYm94L2Y2REJnRlVLalJ4bzhLeDRDWDFpSWQtaW1hZ2VzXzE3NzA3NjQ2NjYyMzZfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwySnBkR052YVc1ZmNHOXlkR1p2YkdsdlgyVnNhWFJsTDJacFozVnlaWE12TURKZmJXOTJhVzVuWDJGMlpYSmhaMlZ6LnBuZyIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc5ODc2MTYwMH19fV19&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=MjBrBOnTttGE6vA-5v~LbICMpnJZb9fMrDX0wZaWPpK8MKPS8LjA45Tvgj-jei1kAhlgRB7WqpV8u4P50I8M1E10gIdgV9cA1xEAoIzJqI66BJRA2RTL0YCqW-YUG-~gcaNXXUsL95g8q-SUTA-9MboGwThTuZiRpiESli8CrgIj0Imx~WJlRhuVsupsOPPgbQfdZKgqkOIno~DTpnrgPPUsnMqjqxKdlJCKR85yGyZ6z9F138j23qbup1hm4c2KOkFPEAK9WRs5U4-G77mrZsYzgZkShwf2L6HDbaA3U2zTOZteLYPM3QfdTWXILH-7pEYsTMcV~izux~ky1VRljA__)

Moving averages help identify prolonged bull and bear regimes and act as systematic entry/exit signals.

### Backtest Performance

![Strategy vs Buy and Hold](https://private-us-east-1.manuscdn.com/sessionFile/XAgjA8hTTgQDFgsMXw39G3/sandbox/f6DBgFUKjRxo8Kx4CX1iId-images_1770764666236_na1fn_L2hvbWUvdWJ1bnR1L2JpdGNvaW5fcG9ydGZvbGlvX2VsaXRlL2ZpZ3VyZXMvMDNfc3RyYXRlZ3lfdnNfaG9sZA.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvWEFnakE4aFRUZ1FERmdzTVh3MzlHMy9zYW5kYm94L2Y2REJnRlVLalJ4bzhLeDRDWDFpSWQtaW1hZ2VzXzE3NzA3NjQ2NjYyMzZfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwySnBkR052YVc1ZmNHOXlkR1p2YkdsdlgyVnNhWFJsTDJacFozVnlaWE12TUROZmMzUnlZWFJsWjNsZmRuTmZhRzlzWkEucG5nIiwiQ29uZGl0aW9uIjp7IkRhdGVMZXNzVGhhbiI6eyJBV1M6RXBvY2hUaW1lIjoxNzk4NzYxNjAwfX19XX0_&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=G2j4~h8PG8DCOLZjp-~iLTdxuGXu1DXzKEcXZLx~fLv2DGJpqDRg0Di~4roDRx0z8lm9XV91h4Y1rFAqesfCamDZ45~S1PLxswgpXhjPRY17gv9PxD~0Vr218TMx5YcnRfTpUXu6K5BR2JVgDKLkuI62XIEm05bCcbBgXb3GElJwzTZjkjWpmGj-8Cr9J2~znSluh9yNa~N~P5SIhf5MxttagoQMTy~oEWnY~R7CDVIszXuE-b9t~2uVPxALByo8vhWweN8e4MLglZTio7soYSv9uSUJiUVIC~HFeVwp9I5f60cB-5LS~1f8PKyt8yoRJKMKXwip2K~-27~gpp9MtQ__)

The trend-following strategy avoids large portions of prolonged downturns, although buy-and-hold achieves higher absolute returns during strong bull cycles.

### Risk Control — Trailing Stop

![Trailing Stop](https://private-us-east-1.manuscdn.com/sessionFile/XAgjA8hTTgQDFgsMXw39G3/sandbox/f6DBgFUKjRxo8Kx4CX1iId-images_1770764666236_na1fn_L2hvbWUvdWJ1bnR1L2JpdGNvaW5fcG9ydGZvbGlvX2VsaXRlL2ZpZ3VyZXMvMDRfdHJhaWxpbmdfc3RvcA.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvWEFnakE4aFRUZ1FERmdzTVh3MzlHMy9zYW5kYm94L2Y2REJnRlVLalJ4bzhLeDRDWDFpSWQtaW1hZ2VzXzE3NzA3NjQ2NjYyMzZfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwySnBkR052YVc1ZmNHOXlkR1p2YkdsdlgyVnNhWFJsTDJacFozVnlaWE12TURSZmRISmhhV3hwYm1kZmMzUnZjQS5wbmciLCJDb25kaXRpb24iOnsiRGF0ZUxlc3NUaGFuIjp7IkFXUzpFcG9jaFRpbWUiOjE3OTg3NjE2MDB9fX1dfQ__&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=mBGfVRh0ZjaTL4QLnSioAsj1ZS~yqjoiQGMxP4iIXsK~WozPp9RKmlRoYCEPG5k1TZtmh5ubrjuOVMa6gosP58wyKmaT2o0DFvx5n4lU8LYIFtOQ-Qj3Nv~2ZbrHHnkqm02KYwwQqcl8XnzgRosPSYC02JdAk7d-2AArdQM4mww1xNHJR-SL7seD40lR71VabCohNy1Mczzd96y7bajgD6dt2wYQusPvFqUlbY3B2fG-9xVpVBGIRMMWouMHWHOilwFsjWU9E4fyReZkDlZswU0JNgjHAoweGEMbMpAAKbGF0J~cAPEqrjSKcOLOaMndFCiikzGOg~0VXz5hZHXggQ__)

Applying a trailing stop-loss significantly reduces major drawdowns while maintaining participation in upward trends.

---

## Key Findings

* Bitcoin is a high-volatility asset unsuitable for passive investors with low risk tolerance.
* Trend-following rules act primarily as **risk management tools**, not return maximizers.
* Buy-and-hold provides the highest long-term returns but with severe drawdowns.
* Systematic strategies reduce time spent in bear markets.
* Trailing stop-loss improves downside protection and capital preservation.

---

## Technical Stack

* Python
* pandas
* numpy
* matplotlib / seaborn
* yfinance

---

## Reproducibility

To reproduce the analysis:

1. Install dependencies
   `pip install -r requirements.txt`

2. Open the notebook
   `notebook/bitcoin_market_analysis.ipynb`

The notebook downloads the data automatically.

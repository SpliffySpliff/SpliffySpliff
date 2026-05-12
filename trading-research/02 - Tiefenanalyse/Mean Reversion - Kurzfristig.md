---
tags: [strategie/meanreversion, strategie/statarb, evidenz/stark, tiefenanalyse]
status: validiert
zeitebene: [intraday, swing]
markt: [equities, etfs]
evidenz: stark
quellen:
  - "Gatev, Goetzmann, Rouwenhorst (2006)"
  - "Connors, Alvarez (2008)"
  - "Chan (2013)"
---

# Mean Reversion — Kurzfristig

> Übertreibungen kehren um. Hohe Win-Rate, aber asymmetrisches Tail-Risiko.

## Funktionsweise
Zwei Hauptzweige:

1. **RSI(2)-Style (Connors)** — Long-Only auf Aktien/ETFs im Uptrend; Kauf bei extrem oversold short-term, Verkauf beim ersten Bounce.
2. **Pairs Trading (Gatev/Goetzmann/Rouwenhorst 2006)** — zwei historisch ko-bewegte Aktien; bei Spread-Divergenz Underperformerin long, Outperformerin short. Vgl. [[Statistical Arbitrage]].

**Ornstein-Uhlenbeck-Modelle** (Chan 2013) formalisieren via stationäre Cointegration-Residuen und expliziter Halbwertszeit `T = ln(2)/θ`.

## Konkrete Regeln (codierbar)

**Connors RSI(2) auf SPY:**
```
Trend-Filter: Close > SMA(200)
Setup:        RSI(2) < 10   (strenger: < 5)
Entry:        Market-Buy auf Close des Signaltages
Exit:         Close > SMA(5)
Position:     fest oder Vola-skaliert
Stop (praktikabel): -3 * ATR(10) vom Entry
```

**Pairs Trading (GGR-Style):**
```
# Formation (12 Monate)
für alle Paare (i,j) im Universum:
    P_norm_i, P_norm_j = preise normalisiert auf $1 am Start
    distanz(i,j) = sum( (P_norm_i - P_norm_j)^2 )
top20 = paare mit kleinster distanz

# Trading (6 Monate)
sigma = std(spread) aus Formation
entry: |spread| > 2*sigma  → mean-reversion-Trade
exit:  spread crossed 0  (Konvergenz) ODER Periodenende
```

**OU-Modell (Chan):**
Schätze `dX = θ(μ - X)dt + σ dW`. **Trade nur wenn Halbwertszeit < 30 Tage** (sonst zu langsam für Edge).

## Empirische Performance
- **GGR (2006):** 1962–2002 US-Stocks, Top-20-Paare: bis zu **11 % annualisierte Excess Returns** auf self-financing-Portfolio nach konservativen Kosten.
- **Do & Faff (2010, Replikation):** Effekt seit 2003 stark abgeschwächt — Top-20 nur noch **30–50 bps p.a.** nach Kosten.
- **Connors/Alvarez (2008):** RSI(2) auf SPY 1993–2008: ~17 % CAGR, Win-Rate 70–80 %, **stark sample-spezifisch**.
- **Aktuelle Replikationen** (QuantifiedStrategies): ~9 % CAGR, ~34 % Max-DD, ~28 % Time-in-Market — Edge deutlich gesunken seit Publikation.

## Fallstricke & Overfitting-Risiken
- **"Picking up pennies in front of a steamroller"**: hohe Win-Rate, gelegentlich katastrophale Verluste (Lehman 2008, COVID März 2020, SVB 2023). Ohne Bankruptcy-Filter ein einziger Tag kann 50 Gewinne löschen.
- **Cointegration bricht zusammen**: fundamentales Event → Halten bis Konvergenz nicht garantiert. **Stop-Loss nötig**.
- **Decay nach Publikation**: Connors RSI(2) hat seit 2008–10 stark an Edge verloren.
- **Hidden Survivorship**: heutiges S&P-500-Universum für 2005er Backtest = systematisch Survivors → fatal für Mean Reversion.
- **Look-ahead in Bands**: Sigma muss aus Formation-, nicht Trading-Periode kommen.
- **Overfitting Lookback**: RSI(2) vs RSI(3) vs RSI(4) — wer alle testet und das beste meldet, hat Bonferroni-Problem (vgl. [[Backtest Biases]]).

## Benötigte Daten/Indikatoren
- Tagesschluss + High/Low (für RSI/ATR)
- **Survivorship-bias-free Universum** mit Delisting
- Borrow-Rates / Short-Availability für Short-Leg (Pairs)
- ADF / Johansen Cointegration-Tests
- Halbwertszeit-Schätzung (OU-Fit)

## Verwandte Notizen
- Kategorie: [[01 - Strategie-Kategorien/Mean Reversion]]
- Verwandt: [[Statistical Arbitrage]]
- Synthese: [[05 - Strategievorschläge/Vorschlag B - Mean Reversion am Value Area Edge]]
- Risiken: [[06 - Risiken & Realität/Backtest Biases]]

## Quellen
- Gatev, Goetzmann, Rouwenhorst (2006): *Pairs Trading: Performance of a Relative-Value Arbitrage Rule*, RFS 19(3) — [PDF](http://stat.wharton.upenn.edu/~steele/Courses/434/434Context/PairsTrading/PairsTradingGGR.pdf)
- Connors & Alvarez (2008): *Short Term Trading Strategies That Work*, TradingMarkets
- Chan, E. (2013): *Algorithmic Trading: Winning Strategies and Their Rationale*, Wiley
- Do & Faff (2010): *Does Simple Pairs Trading Still Work?*, FAJ 66(4)
- StockCharts ChartSchool — [RSI(2)](https://chartschool.stockcharts.com/table-of-contents/trading-strategies-and-models/trading-strategies/rsi-2)

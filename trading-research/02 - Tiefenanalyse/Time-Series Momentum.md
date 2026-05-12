---
tags: [strategie/trend, strategie/momentum, evidenz/stark, tiefenanalyse]
status: validiert
zeitebene: position
markt: [futures, multi-asset]
evidenz: stark
quellen:
  - "Moskowitz, Ooi, Pedersen (2012)"
  - "Hurst, Ooi, Pedersen (2017)"
  - "Faber (2007)"
---

# Time-Series Momentum (TSMOM)

> Quantitative Formalisierung der klassischen Managed-Futures-Trendfolge. Jedes Asset gegen sich selbst — nicht im Querschnitt.

## Funktionsweise
Moskowitz, Ooi, Pedersen (2012): Ein Asset, das in den letzten 12 Monaten **positive Excess-Returns** lieferte, tendiert dazu, im nächsten Monat ebenfalls positiv zu rentieren — und umgekehrt. Im Gegensatz zu [[Cross-Sectional Momentum]] wird **nicht im Querschnitt** verglichen, sondern nur das einzelne Asset gegen seine eigene Vergangenheit.

Operativ: diversifiziertes Portfolio aus Futures (Aktienindex-, Bond-, FX-, Rohstoff-Futures), jeder Kontrakt long/short je nach Vorzeichen seines vergangenen Returns. **Volatilitäts-Skalierung** auf Zielniveau (typisch 40 % annualisiert pro Position) gleicht Risikobudgets aus.

## Konkrete Regeln (codierbar)

```
# MOP 2012 Spezifikation, monatlich
for futures-kontrakt i an Monatsende t:
    r_12m(i,t) = excess return über letzte 12 Monate
    signal(i,t) = sign(r_12m(i,t))                # +1 / -1
    sigma(i,t)  = EWMA-Vol, COM=60 Tage, jährlich skaliert
    position(i,t) = signal(i,t) * (sigma_target / sigma(i,t))
                    # sigma_target = 0.40 pro Leg

portfolio = mean(position over alle i)            # normalisiert auf 10% Portfolio-Vol
rebalance: monatlich, Ausführung t+1 Open
```

**Simplere Faber-Variante** (long-only ETFs):
```
Wenn Close > SMA(10-Monat): kaufen / halten
Sonst: Cash
Anwendung: SPY, EFA, IEF, VNQ, DBC (Ivy Five)
```

**Robustere Hurst/Ooi/Pedersen-Variante:** Kombiniert 1m / 3m / 12m Lookbacks gleichgewichtet ("multi-horizon ensemble").

## Empirische Performance
- **MOP (2012):** 58 liquide Futures, 1985–2009. Brutto-Sharpe ~ **1.43** auf Faktorseite. Signal in 52 von 58 Kontrakten statistisch signifikant. **Beste Performance gerade in extremen Markt-Quartalen** ("crisis alpha"-Eigenschaft).
- **Hurst/Ooi/Pedersen (2017):** 67 Märkte, 1880–2016. **Positive Returns in jedem einzelnen Jahrzehnt** seit 1880. Outperformte in 8 von 10 größten 60/40-Drawdowns. Brutto-Sharpe ~1.0 auf 10 % Vola-Target vor Kosten.
- **Faber (2007):** Ivy-Timing 1973–2005: vergleichbare CAGR wie Buy & Hold (~10 %), aber Max-DD nur **−10 %** statt −45 %.

## Fallstricke & Overfitting-Risiken
- **"Trend Tax" 2011–2019**: SG Trend Index hat lange unterperformt. AQR: "You Can't Always Trend When You Want" (2019) — fehlende ausgedehnte Trends, niedrige Cash-Rates schadeten.
- **Lookback-Tuning**: 1m vs. 3m vs. 12m — wer auf historischem Sample tunt, riskiert Overfitting. Multi-Horizon-Ensemble ist robuster.
- **Slippage**: Klassische Studien rechnen oft unrealistisch niedrig. Real reduziert sich Sharpe um 0.2–0.4. Hurst/Ooi/Pedersen 2017 selbst zieht **~2 % p.a. Kostenabschlag** ab.
- **Whipsaws in Range-Markets**: Bis zu 18-monatige Underwater-Phasen — Retail-Trader kapitulieren vorher (vgl. [[Typische Hobby-Algo-Fehler]]).
- **Survivorship im Futures-Universum**: Manche Backtests ignorieren delistete CBOT-Soft-Commodities.

## Benötigte Daten/Indikatoren
- Tägliche Futures-Settlement-Preise, kontinuierlich verkettet (back-adjusted, panama, ratio)
- Excess Returns über 3M T-Bill (Risk-Free)
- EWMA-Volatilität oder realisierte 60-Tage-Vola
- Optional: SMA(200) / SMA(10-Monat) als Trendfilter

## Verwandte Notizen
- Kategorie: [[01 - Strategie-Kategorien/Trend Following]]
- Synthese: [[05 - Strategievorschläge/Vorschlag A - Futures Trend + Orderflow Filter]]
- Kontrast: [[Cross-Sectional Momentum]]
- Risiken: [[06 - Risiken & Realität/Backtest Biases]]

## Quellen
- Moskowitz, Ooi, Pedersen (2012): *Time Series Momentum*, JFE 104(2) — [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0304405X11002613) · [Preprint](http://docs.lhpedersen.com/TimeSeriesMomentum.pdf)
- Hurst, Ooi, Pedersen (2017): *A Century of Evidence on Trend-Following Investing*, JPM — [AQR](https://www.aqr.com/Insights/Research/Journal-Article/A-Century-of-Evidence-on-Trend-Following-Investing)
- Faber, M. (2007/2013): *A Quantitative Approach to Tactical Asset Allocation*, SSRN 962461 — [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=962461)
- AQR (2019): *You Can't Always Trend When You Want*

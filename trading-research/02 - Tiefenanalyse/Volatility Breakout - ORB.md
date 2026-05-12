---
tags: [strategie/breakout, evidenz/stark, tiefenanalyse]
status: validiert
zeitebene: intraday
markt: [equities, futures]
evidenz: mittel-stark
quellen:
  - "Crabel (1990)"
  - "Zarattini, Aziz (2023)"
  - "Zarattini, Aziz, Barbon (2024)"
---

# Volatility Breakout / Opening Range Breakout (ORB)

> Nach Kompression folgt Expansion. ORB ist eine der wenigen Intraday-Strategien mit kürzlich publizierter, harten OOS-Evidenz.

![[Bilder/orb-setup.svg]]

## Funktionsweise
Volatility-Expansion-Familie: nach Phasen niedriger Volatilität folgt häufig direktionaler Tagesausbruch. **Toby Crabel (1990)** formalisierte das mit der "Stretch" — adaptiver Schwellwert um den Open. **Zarattini et al. (2023–2024)** haben das akademisch reaktiviert mit harten SSRN-Backtests (Sharpe 1.3–2.8 OOS).

## Konkrete Regeln (codierbar)

**Crabel-ORB klassisch (Futures-Tag):**
```
Stretch(t) = SMA_10( min(Open - Low, High - Open) )   # letzte 10 Tage
LongStop   = Open + Stretch
ShortStop  = Open - Stretch
Entry:     Stop-Order wird im Lauf der Session getriggert
Filter:    Nimm Trade NUR nach NR4 oder NR7
           (heutige Range = engste der letzten 4 bzw. 7 Tage)
Exit:      Market-on-Close ODER trailing Stop (PSAR / Vortagestief)
```

**Zarattini/Aziz/Barbon (2023) ORB 5-Min Aktien:**
```
Bar 1 = erste 5-Min-Kerze ab Open (US Equities 09:30–09:35 ET)
Range = High_1 - Low_1
ATR(14) auf Tagesbasis = Sizing-Input

Entry Long:  Bar 1 schließt grün UND nächste Bar bricht über High_1
Entry Short: Bar 1 schließt rot   UND nächste Bar bricht unter Low_1
Stop:        Low_1 (Long) bzw. High_1 (Short)
TP:          10x Risiko ODER Market-on-Close
Sizing:      1% Equity-Risiko/Trade, Hebel bis 4x
Universum:   liquide US-Stocks > $5, ADV > 1M shares, "in play"
```

**Zarattini "Beat the Market" (2024) intraday SPY:**
```
Pro Minute m:
    avg_ret = mean(Return bis Minute m, letzte 14 Tage)
    noise_upper = Open_today * (1 + avg_ret)
    noise_lower = Open_today * (1 - avg_ret)
    # adjustiere um Overnight Gap

Entry @ HH:00 oder HH:30:
    Close(m) > noise_upper → Long
    Close(m) < noise_lower → Short
Exit: Bands + Tages-VWAP als trailing Stop, sonst MOC
```

## Empirische Performance
- **Zarattini/Aziz (2023)** *"Can Day Trading Really Be Profitable?"*: ORB 5-Min Stocks-in-Play 2016–2023, Long-Only 4× Hebel: signifikante Outperformance vs SPY, **Sharpe ~1.5+**.
- **Zarattini/Barbon/Aziz (2024)** *"A Profitable Day Trading Strategy"*: Top-20 Stocks-in-Play, **Sharpe 2.81**, **Total Return >1600 %** (2016–2024), **Alpha 36 % p.a.**.
- **Zarattini/Aziz/Barbon (2024)** *"Beat the Market"* SPY intraday: 2007–2024, **19.6 % p.a., Sharpe 1.33, +1985 %** total **netto Kosten**.

## Fallstricke & Overfitting-Risiken
- **Slippage und Spread auf Open**: Opening Range = dünnster Liquiditäts-Slice des Tages. Backtests mit Mid-Quote überschätzen Returns dramatisch.
- **Survivorship in "Stocks in Play"**: Zarattinis Definition (Gap+News+Volume) ist real-time nicht trivial. Backtests mit heutigem Datensatz haben Hindsight-Bias bei Universum-Auswahl.
- **Hebel-Annahmen**: 4× Margin setzt PDT-konformes Konto voraus (vgl. [[Kapitalanforderungen]]).
- **NR4/NR7-Filter sind überoptimiert**: Crabel's Originalfilter wurden auf genau einem Datenset entwickelt; Replikationen finden den Edge instabil.
- **Regime-Sensitivität**: ORB profitiert von Trendtagen; in Choppy Markets (z.B. 2015) signifikante Strähnen-Verluste.
- **Look-ahead bei Stretch**: Stretch muss aus **Vortags-Daten** kommen, nicht heutigem Open.

## Benötigte Daten/Indikatoren
- Intraday 1- oder 5-Min-Bars (Databento, Polygon, Norgate Intraday)
- Tages-OHLCV für Stretch / NR-Filter / ATR
- **Pre-Market-Volume + News** für "Stocks in Play"-Selection
- Tick-Data oder NBBO-Quotes für **realistische Slippage-Modellierung**
- Optional: Cumulative Volume Delta (CVD) als Bestätigungs-Filter — vgl. [[Vorschlag C - ORB mit CVD-Bestätigung]]

## Verwandte Notizen
- Kategorie: [[01 - Strategie-Kategorien/Breakout]]
- Bestätigung via Order Flow: [[03 - Order Flow/03 - Delta und CVD]]
- Synthese: [[05 - Strategievorschläge/Vorschlag C - ORB mit CVD-Bestätigung]]
- Risiken: [[06 - Risiken & Realität/Backtest Biases]]

## Quellen
- Zarattini, Aziz, Barbon (2024): *Beat the Market: An Effective Intraday Momentum Strategy for SPY*, SSRN 4824172 — [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4824172)
- Zarattini, Aziz (2023): *Can Day Trading Really Be Profitable?*, SSRN
- Zarattini, Barbon, Aziz (2024): *A Profitable Day Trading Strategy For The U.S. Equity Market*, SSRN 4729284 — [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4729284)
- Crabel, T. (1990): *Day Trading with Short Term Price Patterns and Opening Range Breakout*, Traders Press
- StockCharts NR7 — [Link](https://chartschool.stockcharts.com/table-of-contents/trading-strategies-and-models/trading-strategies/narrow-range-day-nr7)

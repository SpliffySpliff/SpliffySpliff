---
tags: [vorschlag, strategie/breakout, strategie/orderflow, synthese]
status: idee
zeitebene: intraday
markt: [equities, futures]
zielmarkt: "SPY/ES + Top-20 Stocks-in-Play"
zielzeitfenster: "M5 für ORB, Tick-Daten für CVD"
evidenz_basis: stark
---

# Vorschlag C — Opening Range Breakout mit CVD-Bestätigung

> **Hauptlogik:** ORB nach Zarattini-Spec (Sharpe 1.3–2.8 OOS in den SSRN-Papern).
> **Order-Flow-Bestätigung:** CVD-Vorzeichen als Filter gegen Fakeout-Breakouts.
> **Volume-Profile-Levels:** Pre-Market-POC als Stop-Referenz.

## Markt & Zeitfenster
- **Universum:**
  - **A**: SPY / ES (Strategie-Engine für Mean-Sharpe)
  - **B**: Top-20 "Stocks-in-Play" (Pre-Market-Gap > 2 %, Volume > Avg × 3, News-Trigger)
- **Signal-Frequenz:** Cash-Open + erste M5-Kerze
- **Holding-Period:** Intraday, MOC-Exit

![[Bilder/orb-setup.svg]]

## Logik im Detail

### Schicht 1 — Stocks-in-Play Selection (für Universum B)
```
Pre-Market (07:00–09:30 ET):
  Gap = (Open_predicted - Close_yesterday) / Close_yesterday
  PMVol = Volume(07:00–09:30) / AvgPMVol(letzte 20 Tage)
  HasNews = bool(News-Headline in letzten 24h)
  
  in_play[t] = (|Gap| > 0.02) AND (PMVol > 3) AND HasNews
```

### Schicht 2 — ORB-Trigger (Zarattini-Aziz-Barbon 2023)
```
Bar 1 = M5 [09:30–09:35]:
  H1 = High_1, L1 = Low_1
  
Direction = 'long'  if Close_1 > Open_1 else 'short'

Trigger Bar 2 [09:35–09:40]:
  Long-Entry:  Direction == 'long'  AND  High_2 > H1
  Short-Entry: Direction == 'short' AND  Low_2  < L1
```

### Schicht 3 — CVD-Bestätigung (Filter, NEU vs. Original)
```
CVD_open_to_trigger = sum( bid_volume - ask_volume,
                            window=[09:30, Trigger-Zeitpunkt] )
                            
Long-Entry zulassen  WENN  CVD > +Threshold
Short-Entry zulassen WENN  CVD < -Threshold
                            
Threshold = 0.5 × StdDev(CVD-Day-Range, letzte 20 Tage)
```
Idee: ohne aggressive Käufer im Breakout-Zeitraum → wahrscheinlich Fakeout.
Vgl. [[03 - Order Flow/03 - Delta und CVD]].

### Schicht 4 — Position-Sizing, Stop, Ziel
```
Risk per Trade = 1% Equity
Stop:           L1 (Long)  oder  H1 (Short)
Position-Size = (Risk_$ ) / (Entry - Stop)
TP:             10x Risk  ODER  Market-on-Close
                # Hebel max 4x nach PDT-Regel
```

### Schicht 5 — Volume-Profile-Trail
Optional: nach Erreichen 3R Profit, Trail-Stop auf **Tages-VWAP** statt fixem Risk. Vgl. [[04 - Volume Profile/03 - VWAP und Anchored VWAP]].

## Erwartete Eigenschaften
- **Baseline (ohne CVD-Filter):** Zarattini-OOS Sharpe ~1.3–2.8
- **Mit CVD-Filter:** sollte False-Positive-Rate senken; aber **muss separat backgetestet werden** — Filter kann auch Edge zerstören
- **Trades/Tag:** ~5–15 (Universum B), 0–1 (Universum A)
- **Realistische Live-Sharpe:** wahrscheinlich deutlich unter den Paper-Werten wegen Slippage / Stocks-in-Play-Selection-Bias

## Trade-offs
| Pro | Contra |
|---|---|
| Härteste publizierte OOS-Evidenz (Zarattini-Serie) | Slippage auf Cash-Open dramatisch |
| CVD-Filter hat plausible Mikrostruktur-Basis | Stocks-in-Play-Selection bei Live nicht trivial |
| Klare, codierbare Regeln | 4×-Hebel-Annahme heikel ohne PDT-Konto |
| Intraday — kein Overnight | Hohe Order-Frequenz → Kommissionen relevant |

## Kapital & Realismus
- **PDT-Regel beachten** ($25k Mindest-Equity bis Juni 2026, danach intraday-proportional) — siehe [[Kapitalanforderungen]]
- **Datenkosten:** Polygon / Databento für intraday + Pre-Market-Daten (~$199/Monat)
- **Live-Slippage** ist der Killer: in Backtest 0.1 % Slippage gerechnet → real 0.3–0.5 % im Open der ersten Minuten

## Konkrete Implementierungs-Schritte
1. **Baseline-ORB ohne CVD** auf Zarattini-Spec replizieren. Wenn nicht reproduzierbar → Daten/Spec-Problem
2. Out-of-Sample 2024–2026 testen, mit konservativer Slippage (mind. 5 bps Stocks, 0.5 Tick Futures)
3. CVD-Filter on/off vergleichen — **Hold-Out-Daten beachten** (vgl. [[Backtest Biases]])
4. Stocks-in-Play-Selection in Live realistisch simulieren (Pre-Market-Daten zum Zeitpunkt der Entscheidung, kein Day-of-Hindsight!)
5. Minimum 3 Monate Paper-Trading, dann Live-Skalierung in 25 %-Schritten

## Verwandte
- [[Volatility Breakout - ORB]]
- [[01 - Strategie-Kategorien/Breakout]]
- [[03 - Order Flow/03 - Delta und CVD]]
- [[Vorschlag A - Futures Trend + Orderflow Filter]]
- [[Vorschlag B - Mean Reversion am Value Area Edge]]
- [[Vergleich und Trade-offs]]

## Quellen
- siehe [[Volatility Breakout - ORB]] (Zarattini-Serie)
- [[03 - Order Flow/03 - Delta und CVD]]

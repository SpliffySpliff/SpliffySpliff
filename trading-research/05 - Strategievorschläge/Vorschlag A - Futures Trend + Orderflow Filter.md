---
tags: [vorschlag, strategie/trend, strategie/orderflow, synthese]
status: idee
zeitebene: [position, swing]
markt: [futures]
zielmarkt: "ES, NQ, CL, ZB, GC, EUR/USD-Futures"
zielzeitfenster: "Daily / 4H Bars für Signal, M1 für Execution"
evidenz_basis: stark
---

# Vorschlag A — Futures Trend Following + Order-Flow-Filter

> **Hauptlogik:** Time-Series-Momentum auf diversifiziertem Futures-Universum.
> **Order-Flow-Filter:** CVD-Bestätigung am Entry, Absorption-Warnung am Exit.
> **Volume-Profile-Levels:** Anchored-VWAP vom Trendbeginn als Trail-Stop.

## Markt & Zeitfenster
- **Universum:** 10–20 liquide Futures (ES, NQ, RTY, CL, NG, GC, SI, HG, ZB, ZN, 6E, 6J, 6B), inkl. Micros (MES/MNQ) für kleinere Konten
- **Signal-Frequenz:** Daily Bar (Settlement)
- **Execution-Frequenz:** nächste Session-Open mit Limit-Order, ggf. M1-Filter via Order Flow
- **Holding-Period:** Wochen bis Monate

## Logik im Detail

### Schicht 1 — TSMOM-Signal (Trendrichtung)
```
Pro Kontrakt i, Ende Tag t:
  r12(i) = Excess Return über letzte 252 Trading-Tage
  r3(i)  = ... letzte 63 Tage
  r1(i)  = ... letzte 21 Tage
  
  signal(i) = mean( sign(r12), sign(r3), sign(r1) )
            ∈ {-1, -0.67, -0.33, 0.33, 0.67, +1}
  # Multi-Horizon-Ensemble (Hurst/Ooi/Pedersen 2017)
```
Vgl. [[Time-Series Momentum]].

### Schicht 2 — Volatilitäts-Sizing
```
sigma(i) = EWMA-Vol (COM=60), annualisiert
target_vol_per_leg = 0.20  # konservativer als MOP-2012
position(i) = signal(i) * (target_vol_per_leg / sigma(i))
```

### Schicht 3 — Order-Flow-Filter (Entry-Veto)
Nur einsteigen / aufstocken, wenn:
```
CVD-Trend(letzte 5 Sessions, M5-Bars) bestätigt das TSMOM-Signal
i.e. signal(i) > 0  AND  CVD-Slope > 0  →  Long OK
     signal(i) < 0  AND  CVD-Slope < 0  →  Short OK
sonst: warten bis nächster Bar
```
Vgl. [[03 - Order Flow/03 - Delta und CVD]].

### Schicht 4 — Volume-Profile-Trail-Stop
Beim Trend-Eintritt: **Anchored VWAP** ab letztem Trend-Reversal-Tief (Long) bzw. -Hoch (Short).
```
Trail-Stop = Anchored VWAP - 1.5 * ATR(20)  (Long)
           = Anchored VWAP + 1.5 * ATR(20)  (Short)
```
Vgl. [[04 - Volume Profile/03 - VWAP und Anchored VWAP]].

### Schicht 5 — Absorption-Warnung (optionaler Reduktor)
Wenn auf höheren Time-Frames (H1) **Stacked Absorption** gegen den Trend in 3+ Sessions in Folge auftritt → Position halbieren (nicht schließen). Vgl. [[03 - Order Flow/04 - Absorption und Exhaustion]].

## Erwartete Eigenschaften
- **Sharpe brutto:** 0.8–1.2 (Multi-Horizon TSMOM-Baseline)
- **Order-Flow-Filter:** soll Whipsaw-Verluste reduzieren — empirisch nicht belegt, deshalb getrennt zu testen!
- **Max Drawdown:** 15–25 %
- **Time-in-Market:** 60–80 %
- **Turnover:** niedrig (monatliche Anpassungen plus gelegentliche OF-Vetos)

## Trade-offs
| Pro | Contra |
|---|---|
| Solide akademische Basis (TSMOM) | Order-Flow-Filter ist unzureichend backgetestet |
| Diversifikation senkt Vola | Daten-/VPS-Kosten hoch ([[Kosten und Infrastruktur]]) |
| Skalierbar mit Kapital | Hat 18-Mon-Underwater-Phasen — Disziplin nötig |
| MES/MNQ erlaubt kleinen Kapitalstart | OF-Filter könnte spuriously fitten |

## Kapital & Realismus
- **Minimum:** ~$25k mit Micros (1 MES, 1 MNQ, 1 MGC)
- **Komfortabel:** $100k+ für volle Diversifikation
- vgl. [[Kapitalanforderungen]], [[Realistische Erfolgsraten]]

## Konkrete Implementierungs-Schritte (für späteren Algo)
1. TSMOM-Baseline ohne OF-Filter implementieren und backtesten (1990–2020 Train, 2021–2025 Holdout)
2. Slippage realistisch modellieren (vgl. Hurst/Ooi/Pedersen 2017: ~2 % p.a. Abschlag)
3. **Erst dann** OF-Filter einzeln on/off vergleichen — sonst Bonferroni-Falle (vgl. [[Backtest Biases]])
4. Live in Paper-Trading **3 Monate**, bevor echtes Geld
5. DSR berechnen vor Live-Going

## Verwandte
- [[Time-Series Momentum]]
- [[01 - Strategie-Kategorien/Trend Following]]
- [[Vorschlag B - Mean Reversion am Value Area Edge]]
- [[Vorschlag C - ORB mit CVD-Bestätigung]]
- [[Vergleich und Trade-offs]]

## Quellen
- siehe [[Time-Series Momentum]] und [[03 - Order Flow/03 - Delta und CVD]]

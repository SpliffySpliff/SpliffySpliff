---
tags: [vorschlag, strategie/meanreversion, strategie/volumeprofile, strategie/orderflow, synthese]
status: idee
zeitebene: intraday
markt: [futures]
zielmarkt: "ES, NQ, CL (Liquidität entscheidend)"
zielzeitfenster: "M5 / M15 Bars, Daily Volume Profile"
evidenz_basis: mittel
---

# Vorschlag B — Mean Reversion am Value Area Edge

> **Hauptlogik:** Intraday-Mean-Reversion in Range-Days, getradet an VAH/VAL.
> **Order-Flow-Bestätigung:** Absorption am Edge als Trigger.
> **Volume-Profile-Levels:** POC als Profit-Target.
> **Volatilitäts-Regime-Filter:** nur an Tagen mit IB-basiertem Range-Verdacht.

## Markt & Zeitfenster
- **Universum:** 1–3 liquide Futures (ES, NQ, CL — wegen klarer Volumen-Konzentration)
- **Signal-Frequenz:** M5 / M15 Bars
- **Holding-Period:** Minuten bis wenige Stunden, Cut Market-on-Close
- **Sessions:** US-Cash-Session (RTH)

![[Bilder/volume-profile-schema.svg]]

## Logik im Detail

### Schicht 1 — Regime-Filter (Trade-Tag-Auswahl)
Tagestyp bestimmen nach ersten **60 Min Initial Balance (IB)**:
```
IB_high  = High der ersten 60 Min
IB_low   = Low  der ersten 60 Min
IB_range = IB_high - IB_low

Open-Type erkennen (Dalton):
  Open-Drive       → KEIN Trade (Trendtag wahrscheinlich)
  Open-Test-Drive  → KEIN Trade
  Open-Auction     → TRADE OK
  Open-Rejection-Reverse → TRADE OK
```
Vgl. [[04 - Volume Profile/04 - Market Profile TPO]].

### Schicht 2 — Volume Profile aufbauen (laufend)
- Composite gestern + Open-Profile heute
- **VAH** (Value Area High), **VAL** (Value Area Low), **POC** identifizieren
- Vgl. [[04 - Volume Profile/02 - POC Value Area VAH VAL]]

### Schicht 3 — Setup-Trigger
**Long-Setup (Fade VAL):**
```
1. Preis touched VAL (oder leicht darunter, max −0.25 × Average-True-Range)
2. Footprint zeigt Absorption: starke Bid-Volumen UND Preis hält (kein new low)
3. Stacked Imbalances auf Bid-Seite (3+ in Folge)
4. CVD lokal flach oder positiv (kein anhaltender Verkaufsdruck)
```
**Short-Setup (Fade VAH):** spiegelbildlich.

Vgl. [[03 - Order Flow/04 - Absorption und Exhaustion]] und [[03 - Order Flow/02 - Bid-Ask Imbalance]].

### Schicht 4 — Entry, Stop, Ziel
```
Entry:  Market-Order beim Absorption-Trigger
Stop:   1.0 × ATR(15) jenseits des Edge (VAL-Trigger → Stop unter Tief der Absorption-Kerze)
Ziel 1: POC (50% Position schließen)
Ziel 2: gegenüberliegender Edge (VAH bei Long-Trade)
        ODER Trail mit M5-Swing-Lows nach Erreichen Ziel 1
Hard-Cut: Market-on-Close, Übernacht NICHT halten
```

### Schicht 5 — Anti-Trend-Schutz
**Veto-Bedingung** (Tag wechselt zu Trend):
- Wenn Preis VAH überschreitet und dort 30 Min hält (Acceptance) → keine Long-Fades mehr
- Wenn CVD klar diverging und beschleunigend → bestehende Position schließen

## Erwartete Eigenschaften
- **Win-Rate:** 55–65 % (typisch für gut gefilterte Range-Strategien)
- **R/R:** ~1:1 bis 1:1.5
- **Trades/Tag:** 0–3
- **Filter-Quote:** ~40–60 % der Tage werden gar nicht getradet (Trendtage)
- **Max Drawdown:** moderat, da kleine Trades

## Trade-offs
| Pro | Contra |
|---|---|
| Saubere Logik (Auction-Market-Theory) | Wenig peer-reviewed Evidenz für VP-Edges ([[01 - Strategie-Kategorien/Volume Profile Ansätze]]) |
| Order Flow gibt zusätzlichen Konfirmations-Layer | Diskretionär in Komponenten — schwer pur algorithmisch |
| Tageshorizont = kein Overnight-Risiko | Slippage und Kommissionen kritisch (viele Trades) |
| | Funktioniert nur in Range — Regime-Filter muss präzise sein |

## Kapital & Realismus
- **Minimum:** $25k für MES-Trading
- **Daten:** CME Real-Time + Order-Flow-Visualisierung (ATAS, Bookmap, Sierra Chart)
- vgl. [[Kosten und Infrastruktur]]

## Konkrete Implementierungs-Schritte
1. **Regime-Filter zuerst validieren**: Was war historische Trefferquote für "Range-Tag-Klassifikation" via IB + Open-Type? (Backtest ohne OF zuerst)
2. Volume-Profile in Code: typischerweise via Tick-Daten (Databento, Sierra Chart) — VPVR rekonstruieren
3. Order-Flow-Layer **separat hinzufügen und vergleichen** — Bonferroni!
4. Realistische Slippage: ES Tick = $12.50, an Range-Edges kann Slippage 1–2 Ticks sein
5. Backtest-Periode mit echtem Range-Markt-Anteil (z.B. 2017, 2019, 2023 Sommer)

## Verwandte
- [[Mean Reversion - Kurzfristig]]
- [[04 - Volume Profile/02 - POC Value Area VAH VAL]]
- [[04 - Volume Profile/05 - Kombinierte Anwendung]]
- [[03 - Order Flow/04 - Absorption und Exhaustion]]
- [[Vorschlag A - Futures Trend + Orderflow Filter]]
- [[Vorschlag C - ORB mit CVD-Bestätigung]]
- [[Vergleich und Trade-offs]]

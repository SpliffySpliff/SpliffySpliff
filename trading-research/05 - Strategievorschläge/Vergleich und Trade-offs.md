---
tags: [vorschlag, vergleich, entscheidung]
status: idee
---

# Vergleich der drei Vorschläge

![[Bilder/strategie-decision-tree.svg]]

## Auf einen Blick

| Kriterium | [[Vorschlag A - Futures Trend + Orderflow Filter\|A — Trend + OF]] | [[Vorschlag B - Mean Reversion am Value Area Edge\|B — MR @ VA Edge]] | [[Vorschlag C - ORB mit CVD-Bestätigung\|C — ORB + CVD]] |
|---|---|---|---|
| **Markt** | Futures (multi-asset) | Futures (ES/NQ/CL) | Equities + Futures |
| **Zeitebene** | Position–Swing | Intraday | Intraday |
| **Frequenz** | wenige Trades/Monat | 0–3 Trades/Tag | 5–15 Trades/Tag |
| **Evidenz-Basis** | **stark** (TSMOM-Papers) | mittel (VP eher Praxis) | **stark** (Zarattini-Papers) |
| **Min. Kapital** | $25k mit Micros | $25k mit MES | $25k (PDT) |
| **Daten-Anspruch** | Daily OHLC + M5 für OF | Tick-Daten für VP+OF | Intraday + Pre-Market |
| **Komplexität** | mittel | hoch | mittel |
| **Erwarteter Sharpe (netto)** | 0.4–0.8 | 0.5–1.0 | unklar (Paper: 1.3+) |
| **Skalierbarkeit** | hoch | mittel | mittel |
| **Psychologische Härte** | mittel (Wochen-Trades) | hoch (schnelle Entscheidungen) | hoch (Open-Stress) |
| **Hauptrisiko** | Whipsaw / "Trend Tax" | Filter falsch → Trendtag verlieren | Slippage / Selection-Bias |

## Welcher Vorschlag passt zu welchem Profil?

### Wenn du **Anfänger** im Algo-Trading bist
→ **Vorschlag A** (Time-Series Momentum)
- Niedrigste Frequenz, viel Zeit für Reflektion
- Robusteste Evidenz seit 1880 (Hurst/Ooi/Pedersen 2017)
- Wenig Datenanspruch in Basis-Variante
- OF-Layer ist optional — kann später dazukommen

### Wenn du **Vollzeit-Day-Trading** anstrebst und Geduld für VP/OF-Lernkurve hast
→ **Vorschlag B** (Mean Reversion @ VA Edge)
- Höchster Tagesaufwand, aber lehrreichster Mikrostruktur-Einblick
- Niedrigster Hebel — psychologisch verträglicher
- Aber: VP-Edge **weniger akademisch gestützt** als die anderen

### Wenn du **maximale erwartete Performance** willst und Risiko aushältst
→ **Vorschlag C** (ORB + CVD)
- Höchste publizierte Sharpe-Werte (Zarattini)
- Aber: **Live-Replikation ist schwer** wegen Slippage und Stocks-in-Play-Selection
- Realistische Live-Sharpe wahrscheinlich 30–50 % unter Paper-Werten

## Kombinierbarkeit
Die drei sind **nicht stark korreliert** — Kombi-Portfolio möglich:
- A liefert Position-Trading-Basis
- C liefert Intraday-Alpha an günstigen Tagen
- B als Range-Day-Spezialist

→ Aber: drei Strategien parallel = 3× Implementations-/Monitoring-Aufwand. Für Solo-Quant **erst eine sauber zum Laufen bringen**.

## Empfehlung für den Aufbau

```
Phase 1 (Monat 1–3):  Vorschlag A Baseline (ohne OF-Filter)
                      → Backtest 1990–2020, Holdout 2021–2025
                      → Paper-Trade 3 Monate

Phase 2 (Monat 4–6):  Vorschlag A + OF-Filter
                      → Layer separat testen, DSR-Adjustment

Phase 3 (Monat 7–12): Vorschlag C dazu (Stocks-in-Play-ORB)
                      → kapitalbedarf-bedingt nur falls A profitabel läuft

Phase 4 (Monat 12+):  Vorschlag B nur, wenn VP/OF wirklich verstanden
                      → höchste diskretionäre Komponente
```

## Verwandte
- [[Vorschlag A - Futures Trend + Orderflow Filter]]
- [[Vorschlag B - Mean Reversion am Value Area Edge]]
- [[Vorschlag C - ORB mit CVD-Bestätigung]]
- [[Realistische Erfolgsraten]]
- [[Typische Hobby-Algo-Fehler]]
- [[Kapitalanforderungen]]
- [[Kosten und Infrastruktur]]

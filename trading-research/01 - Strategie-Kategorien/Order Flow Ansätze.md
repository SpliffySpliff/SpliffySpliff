---
tags: [strategie/orderflow, orderflow, evidenz/mittel, kategorie]
status: recherche
zeitebene: [scalping, intraday]
evidenz: mittel
quellen:
  - "Easley, Lopez de Prado, O'Hara (2012)"
  - "Cont, Kukanov, Stoikov (2014)"
  - "Bouchaud et al. (2018)"
---

# Order-Flow-basierte Ansätze

> Analyse der tatsächlichen Trades und Order-Book-Dynamik — Aggressor-Side, Bid/Ask-Volumen, Iceberg-Detektion.

## Grundidee
Statt nur OHLC-Preise zu sehen: **wer hat aggressiv gehandelt, in welcher Größe, auf welcher Seite?** Aggressive Käufer/Verkäufer treiben den Preis kurzfristig. Mikrostruktur-Forschung belegt: Order Flow Imbalance hat **statistisch signifikanten Preis-Impact** (Cont/Kukanov/Stoikov 2014).

## Marktbedingungen
- Liquide Futures (ES, NQ, CL, Bund, Gold)
- Aktien mit transparenter Tick-Data (US Cash Equities mit konsolidiertem Tape)
- Kurzfristige Signale; beste Wirkung bei **mittlerer** Volatilität
- Schlechter in fragmentierten Märkten ohne konsolidiertes Tape (FX, einige Crypto-Pairs)

## Schwächen
- **Sehr datenintensiv** (Level-2/Level-3, oft kostenpflichtig)
- HFT konkurriert aggressiv um dieselben Signale
- **Spoofing/Layering** verzerrt Signale im DOM (Quote-Stuffing seltener nach Dodd-Frank, aber existent)
- Schwer in vollständige Strategie zu systematisieren — viele diskretionäre Trader scheitern an Disziplin
- In Crypto teils gestreut über Exchanges → unvollständige Sicht
- Marketing-getriebene Edu-Industrie (Bookmap, ATAS) übertreibt Signal-Edge

## Zeitebenen
Scalping und Intraday (Sekunden–Stunden). Selten Swing.

## Sub-Varianten
- **Footprint-/Cluster-Charts** — siehe [[03 - Order Flow/01 - Footprint Charts]]
- **Cumulative Delta** — siehe [[03 - Order Flow/03 - Delta und CVD]]
- **Order Flow Imbalance (OFI)** — Cont/Kukanov/Stoikov, Standardmaß
- **VPIN** (Volume-Synchronized Probability of Informed Trading) — Easley/LdP/O'Hara
- **DOM-Reading / Tape Reading** (klassisch, diskretionär)

## Verwandte Notizen
Alle Details:
- [[03 - Order Flow/01 - Footprint Charts]]
- [[03 - Order Flow/02 - Bid-Ask Imbalance]]
- [[03 - Order Flow/03 - Delta und CVD]]
- [[03 - Order Flow/04 - Absorption und Exhaustion]]
- [[03 - Order Flow/05 - Order Book Analyse DOM Bookmap]]
- [[03 - Order Flow/06 - Tools und Datenquellen]]

## Quellen
- Easley, Lopez de Prado, O'Hara (2012): *Flow Toxicity and Liquidity in a High-Frequency World*, RFS 25(5) — [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1695596)
- Cont, Kukanov, Stoikov (2014): *The Price Impact of Order Book Events*, JFE 12(1)
- Bouchaud, Bonart, Donier, Gould (2018): *Trades, Quotes and Prices*, Cambridge University Press

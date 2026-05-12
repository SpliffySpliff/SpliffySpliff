---
tags: [risiko, kosten, infrastruktur, daten]
status: recherche
warnung: "Preise Stand Mai 2026, Volatil — am Live-Anbieter prüfen"
quellen:
  - "CME Market Data Fee List (Jan 2026)"
  - "IBKR Pricing Pages"
  - "Databento, Bookmap Pricing"
---

# Kosten und Infrastruktur

> Was kostet ernsthaftes Retail-Quant-Trading wirklich? **Vorab-Hurdle: $3.000–6.000 p.a. fixe Kosten**, bevor ein einziger Trade gemacht wird.

## Marktdaten

| Posten | Kosten (Mai 2026, Annäherung) |
|---|---|
| **CME Real-Time Non-Pro** (via Broker aggregiert) | ca. **$12–15/Monat** pro Exchange |
| **CME Real-Time Pro** | **$140/Monat** pro Exchange |
| **Databento Standard** | **$199/Monat** unlimited (CME only: $179) + PAYG für Historical |
| **Norgate Premium Data** (US-Aktien survivorship-frei) | **$60–80/Monat** je nach Region |
| **Polygon Stocks Developer** | ~$199/Monat |
| **IBKR Market Data Bundles** | $0–$50/Monat je nach Bundle |

⚠️ **Validieren am Live-Anbieter:** [CME Fee List Jan 2026](https://www.cmegroup.com/market-data/files/january-2026-market-data-fee-list.pdf), [Databento Pricing](https://databento.com/pricing).

## Brokerage / Kommissionen (IBKR Tiered)

| Asset | Kommission |
|---|---|
| **US-Aktien** | $0.0035/Share, min $0.35/Order |
| **ES Futures Roundtrip** | ~$4.50 ($0.85 IBKR + $1.38 CME + $0.02 Reg, plus Slippage) |
| **MES Roundtrip** | ~**$1.10–1.30** |

→ Bei 10.000 Trades/Jahr auf MES: **$11.000–13.000 Kommissionen** allein.

## Plattformen / Tools

| Tool | Kosten/Monat | Use-Case |
|---|---|---|
| **Bookmap Global** | $49 (oder $39 jährlich) | Heatmap, Liquidity-Visualisierung |
| **Bookmap Global+** | $99 | + Order-Flow-Indikatoren |
| **Bookmap Lifetime** | $1.990 einmalig | wer dauerhaft bleibt |
| **ATAS Plus / Pro** | ~$25 / ~$70 | Footprint, Cluster-Charts — *Preise via Drittquelle, prüfen* |
| **Sierra Chart Standard** | ab **$26** | leichtgewichtig, gut für Skripting |
| **NinjaTrader Lifetime** | ~$1.499 | populär für Futures-Retail |
| **Quantower** | $54+ | Multi-Asset, Footprint |
| **Jigsaw** | $147/Jahr | DOM-Trading-fokussiert |

→ Data extra bei den meisten.

## Hosting / Latency

| Anbieter | Kosten/Monat | Latenz zu CME Aurora |
|---|---|---|
| **TraderVPS** | $60–150 | <1 ms |
| **QuantVPS** | $59–199 | <1 ms |
| **Generic AWS/GCP** | $20–80 | 5–30 ms (je nach Region) |

Für **HFT/Market Making**: Colocation in CME Aurora, **mehrere tausend $/Monat** — außerhalb Retail.

## Jahres-Budget-Beispiel (Retail-Quant, ernsthaft)

| Posten | Annahme | Jährlich |
|---|---|---|
| Datenfeed (CME Non-Pro via Broker) | $15/Mon | $180 |
| Norgate Stocks PIT-Data | $70/Mon | $840 |
| VPS | $80/Mon | $960 |
| Bookmap Global | $49/Mon | $588 |
| Backtesting-Library (mlfinlab, kostenlos) | — | $0 |
| Misc (Tools, Books, Courses) | | $500 |
| **Summe fix** | | **~$3.070** |
| Kommissionen MES @ 5k Trades | $1.20 × 5k | $6.000 |
| **Gesamt** | | **~$9.000 p.a.** |

→ Bei **$25.000 Konto**: **36 % Vorab-Hurdle** vor Gewinn-Schwelle. Bei $50k: 18 %. Bei $100k: 9 %.

**Implikation:** Quant-Strategien skalieren erst ab **$50k–100k** wirtschaftlich. Darunter werden Fixkosten zum Strategie-Killer.

## Verwandte Notizen
- [[Kapitalanforderungen]]
- [[Realistische Erfolgsraten]]
- Order-Flow-Tools im Detail: [[03 - Order Flow/06 - Tools und Datenquellen]]

## Quellen
- CME January 2026 Market Data Fee List — [PDF](https://www.cmegroup.com/market-data/files/january-2026-market-data-fee-list.pdf)
- IBKR Futures Commissions — [Link](https://www.interactivebrokers.com/en/pricing/commissions-futures.php)
- IBKR Stock Commissions — [Link](https://www.interactivebrokers.com/en/pricing/commissions-stocks.php)
- Databento Pricing — [Link](https://databento.com/pricing)
- Bookmap Packages — [Link](https://bookmap.com/packages-comparison)
- AMP Futures Margins — [Link](https://www.ampfutures.com/trading-info/margins)

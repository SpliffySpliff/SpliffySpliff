---
tags: [risiko, kapital, regulierung]
status: recherche
quellen:
  - "FINRA Notice 26-10"
  - "CME Margin Files"
  - "Thorp / MacLean / Ziemba"
---

# Kapitalanforderungen & Risk-of-Ruin

## US-Aktien-Day-Trading: PDT-Regel
**Pattern-Day-Trader-Regel** (FINRA) — wer **≥4 Day-Trades in 5 Geschäftstagen** macht und das **>6 %** aller Trades sind, brauchte historisch mindestens **$25.000 Margin-Equity** dauerhaft.

> [!info] Update Juni 2026
> Per FINRA-Notice 26-10 wird die feste $25k-Schwelle **ab 4. Juni 2026** durch eine intraday-exposure-proportionale Equity-Anforderung ersetzt; Mindestkonto wieder nur die regulären **$2.000 Margin-Mindestanforderung**. Implementierungs-Phase bei Brokern bis Oktober 2027.
>
> ⚠️ Status zum Lesedatum prüfen — Quelle: [FINRA Notice 26-10](https://www.finra.org/rules-guidance/notices/26-10).

## Futures (USA, CME) — keine PDT-Regel

Stand April 2026 (Annäherung, **am CME Margin File validieren**):

| Kontrakt | Initial Margin (Overnight) | Intraday Margin (typ.) |
|---|---|---|
| **ES** (E-Mini S&P 500) | ~$13.200 | ~$500 (AMP, NinjaTrader) |
| **MES** (Micro E-Mini S&P) | ~$1.320 | ~$50 |
| **NQ** Maintenance | ~$36.887 | je Broker |
| **MNQ** | ~$3.690 | ~$100 |

**Realistische Untergrenze fürs Futures-Day-Trading:**
- 1 MES/MNQ Kontrakt, 1–2 % Risiko/Trade: **$10.000–$25.000**
- 1 ES (Großkontrakt): **mindestens $50.000+**, sonst Risk-of-Ruin bei normalem DD >50 %

## Kelly Criterion & Risk-of-Ruin

**Full-Kelly:** `f* = (b·p − q) / b`

Bei realistischer Edge-Strategie (Win-Rate 55 %, R/R 1.2): `f* ≈ 13 %` pro Trade. Bei Schätzfehler & Korrelation führt das zu **50%+ Drawdowns** (Thorp, MacLean/Ziemba).

**Standard-Empfehlung: Half-Kelly oder Quarter-Kelly.**

### Risk-of-Ruin-Heuristik
Bei **1 % Risiko/Trade** braucht man ~**50R Equity-Cushion** (50 max-Verlust-R), um durch eine 95-Perzentil-Losing-Streak (10–15 Trades in Folge Verlust) durchzukommen.

```
Mindestkonto ≈ 50 × (Risk_pro_Trade) / (Risk_Prozent_Equity)

Beispiel: Risk 1% Equity, Strategie verliert max. €200/Trade
          → Mindestkonto ≈ 50 × €200 / 0.01 = €1.000.000? NEIN —
          Berechnung anders herum:
          50 max-R = 50 Stop-Outs → 50 × 1% = 50% MaxDD
          → Wer 50% MaxDD nicht überlebt, ist unterkapitalisiert
```

Konkret: Bei Risk 1 % / Trade und 50 % Equity-Toleranz: **du tolerierst ~50 Stops in Folge**. Hat deine Strategie historisch je 30 Verlust-Trades am Stück gehabt → Strategie nicht skalierbar.

## Empfehlung für Anfänger-Quant
- **Paper-Trading** für mindestens 3 Monate (Live-Slippage simulieren)
- **MES/MNQ statt ES/NQ** wegen 1/10-Kontraktgröße
- **Maximaler täglicher Verlust** = 2–3 R, dann Hard-Stop für den Tag
- **Korrelierte Positionen** zählen als eine — keine doppelte Exposure durch ES+NQ+YM gleichzeitig

## Verwandte Notizen
- [[Realistische Erfolgsraten]]
- [[Kosten und Infrastruktur]]
- [[Typische Hobby-Algo-Fehler]]

## Quellen
- FINRA Notice 26-10 — [Link](https://www.finra.org/rules-guidance/notices/26-10)
- AMP Futures Margins — [Link](https://www.ampfutures.com/trading-info/margins)
- Thorp, E.O. (2006): *The Kelly Capital Growth Investment Criterion*
- MacLean, Thorp, Ziemba (eds., 2011): *The Kelly Capital Growth Investment Criterion*

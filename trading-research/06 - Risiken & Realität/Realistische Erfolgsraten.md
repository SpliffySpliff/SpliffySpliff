---
tags: [risiko, kritisch, evidenz/stark]
status: validiert
quellen:
  - "Barber, Odean (2000)"
  - "Chague, De-Losso, Giovannetti (2020)"
  - "ESMA (2018)"
---

# Realistische Erfolgsraten — Die Zahlen sind brutal

> [!warning] Ehrliche Antwort
> In den meisten dokumentierten Stichproben verliert die **deutliche Mehrheit** der Retail-Trader Geld. Im Day-Trading liegen die echten Verlierer-Quoten bei **95–99 %**, nicht bei 80–90 %.

## Die Studien

### Barber & Odean (2000) — "Trading Is Hazardous to Your Wealth"
- 66.465 US-Discount-Broker-Haushalte, 1991–1996
- Durchschnittshaushalt: **16.4 % p.a.** (Markt: 17.9 %)
- **Aktivste 20 %** (höchster Turnover): nur **11.4 %** — Underperformance-Gap **6.5 pp p.a.**
- Erklärung: Trading-Kosten + schlechte Selektion

### Chague, De-Losso, Giovannetti (2020) — "Day Trading for a Living?"
Brasilianischer Aktien-Futures-Markt (drittgrößter weltweit), **alle Neueinsteiger 2013–2015 mit ≥300 Trading-Tagen**:
- **97 % verloren Geld**
- Nur **1.1 %** verdienten mehr als den brasilianischen Mindestlohn
- Nur **0.5 %** mehr als Einstiegsgehalt eines Bankkassierers
- Erfolgreichster Trader: US$ 310/Tag — bei extremem Risiko
- **Keine Evidenz für "Lernen" durch Trading-Praxis** in Regressionen auf Erfahrung

### ESMA (2018) — CFD-Restriktions-Grundlage
Über EU-NCAs gemittelt:
- **74–89 % der Retail-CFD-Konten verlieren Geld**
- Mittlere Verluste pro Konto **€1.600 bis €29.000**
- Konsequenz: Hebel-Cap (30:1 Major-FX → 2:1 Crypto), Margin-Close-out, Negative-Balance-Protection

### Barber et al. (2014, Taiwan)
Nur **~1 %** der Day-Trader produzieren langfristig vorhersagbar profitable Renditen nach Kosten.

## Realistische Erwartungen für Quant-Strategien

Wenn jemand "Sharpe 2.0+" verspricht: **rotes Tuch**. Realistisch erreichbar für gut umgesetzte Faktor-Strategien (TSMOM, XSMOM):

| Strategie | Realistischer **Brutto**-Sharpe | Realistischer **Netto**-Sharpe |
|---|---|---|
| Time-Series Momentum, diversifiziertes Futures-Portfolio | 0.8–1.4 | 0.4–0.8 |
| Cross-Sectional Momentum, Large-Cap-Equities | 0.5–0.7 | 0.2–0.5 |
| Mean Reversion, kurzfristig | 0.8–1.5 (vor Decay) | 0.3–0.8 |
| ORB Stocks-in-Play (Zarattini) | 1.3–2.8 (Paper-OOS) | unbekannt im Live-Trading |
| Market Making Retail | meist negativ | meist negativ |

## Verwandte Notizen
- [[Typische Hobby-Algo-Fehler]]
- [[Backtest Biases]]
- [[Kapitalanforderungen]]
- [[Smart Money Concepts ICT]] — Branchen-Anreize für Retail-Promises

## Quellen
- Barber & Odean (2000): *Trading Is Hazardous to Your Wealth*, JoF — [PDF](https://faculty.haas.berkeley.edu/odean/papers%20current%20versions/individual_investor_performance_final.pdf)
- Chague, De-Losso, Giovannetti (2020): *Day Trading for a Living?*, SSRN 3423101 — [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3423101)
- ESMA (2018): CFD/Binary-Options Press Release — [ESMA](https://www.esma.europa.eu/press-news/esma-news/esma-agrees-prohibit-binary-options-and-restrict-cfds-protect-retail-investors)
- Barber et al. (2014): *The Cross-Section of Speculator Skill: Evidence from Taiwan*

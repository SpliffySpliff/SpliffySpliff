---
tags: [risiko, kritisch, fehler]
status: validiert
quellen:
  - "Bailey, Lopez de Prado (2014)"
  - "Lopez de Prado (2018)"
  - "Harvey, Liu, Zhu (2016)"
---

# Typische Hobby-Algo-Fehler

> Sortiert nach Häufigkeit. Wer diese 7 vermeidet, ist bereits weit vor 90 % der Retail-Algos.

## 1. Overfitting durch Parameter-Mining
> "Ich teste RSI von 2 bis 30, MAs von 5 bis 200 — der Sharpe-2.5-Sweetspot ist Noise."

**Bailey et al. (2014):** Bei N Trials ist die erwartete Maximum-Sharpe-Ratio rein zufällig:
$$E[\max SR] \approx \sqrt{2 \ln N} \cdot \sigma_{SR}$$

Bei 100 Variationen und annualisiertem $\sigma_{SR} \approx 0.5$ → erwartete maximale SR von **~1.4 — ohne jeden echten Edge**.

**Gegenmaßnahme:** Deflated Sharpe Ratio (siehe [[Backtest Biases]]).

## 2. Kein Out-of-Sample / Walk-Forward
Backtest auf 2010–2024, live deployt 2025 → Modell crasht, weil Marktregime gewechselt hat.

**Korrekt:**
- Train: 2010–2018
- Validation: 2019–2021
- **Holdout (unangetastet bis nach Modellfreeze): 2022–2024**

## 3. Slippage & Kommissionen unterschätzt
Bei MES nur `$0.85/Kontrakt` eingerechnet? Falsch. Real:
- IBKR-Kommission: $0.85
- CME-Exchange-Fee: $1.38
- Regulatory: $0.02
- Slippage 0.25–0.5 Ticks ≈ $1.25–2.50

→ **Roundtrip real ~$4.50** statt $1.70. Bei 10.000 Trades/Jahr macht das **$28.000 Kostenunterschied**.

## 4. Survivorship Bias
S&P-500-Universum von **heute** für 2010er Backtest:
- Lehman ist nicht drin (gegangen 2008)
- Wirecard ist nicht drin (gegangen 2020)
- Bear Stearns, Enron, ... alle weg

→ Strategien sehen **1.5–2 % p.a. zu hohen Return**. CRSP-Daten zeigen **1.6 pp Differenz** zwischen Survivorship-frei und -biased (1926–2001).

**Lösung:** Point-in-Time-Daten (CRSP, Norgate, Compustat mit historischen Snapshots).

## 5. Look-ahead Bias
Klassische Fallen:
- `SMA(200) ab heutigem Close` verwendet — aber Close ist erst nach Marktschluss bekannt. Order auf `Close ≥ SMA(200)` muss bis nächste Open warten.
- Fundamentaldaten ohne Veröffentlichungs-Lag (Q4-Earnings sind erst Mitte Februar bekannt, nicht 31.12.).
- Pair-Selection in Pairs-Trading mit Daten aus der Trading-Periode.
- Z-Score-Normalisierung über das **ganze** Sample statt rolling.

## 6. Data Snooping
Selber Investor liest 5 Quant-Bücher, baut 5 Strategien auf demselben SPY-Datensatz → Bonferroni-korrigierte Signifikanz viel schwächer als einzelne p-Werte suggerieren.

**Harvey/Liu/Zhu (2016):** Historische Faktor-Literatur ignoriert Bonferroni massiv. Realistischer Schwellwert für "neue" Faktor-t-Stat: **|t| > 3.0**, nicht 2.0.

## 7. In-Sample/Out-of-Sample-Leakage
Walk-Forward implementiert, aber **Feature-Normalisierung (mean/std) auf Gesamt-Datensatz** gefittet → "OOS" sieht insgeheim die Verteilung der Zukunft.

**Andere subtile Leaks:**
- Target-Encoding mit Future-Mean
- Bei TS-CV: Train-Test ohne Embargo (Trade-Overlap zwischen Train-Ende und Test-Beginn)
- Hyperparameter-Tuning mit Test-Set-Feedback ("ich probiere noch eins, das ja bekanntermaßen 2024 schlecht lief")

## Verwandte Notizen
- [[Backtest Biases]] — formale Gegenmaßnahmen
- [[Kosten und Infrastruktur]]
- [[Realistische Erfolgsraten]]
- [[Kapitalanforderungen]]

## Quellen
- Bailey & Lopez de Prado (2014): *The Deflated Sharpe Ratio*, JPM — [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2460551)
- Lopez de Prado, M. (2018): *Advances in Financial Machine Learning*, Wiley
- Harvey, Liu, Zhu (2016): *...and the Cross-Section of Expected Returns*, RFS 29(1)

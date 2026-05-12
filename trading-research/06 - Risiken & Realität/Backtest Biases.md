---
tags: [risiko, kritisch, methodik, paper]
status: validiert
quellen:
  - "Bailey, Lopez de Prado (2014)"
  - "Bailey, Borwein, Lopez de Prado, Zhu (2015)"
  - "Harvey, Liu, Zhu (2016)"
---

# Backtest Biases — Formale Gegenmaßnahmen

> Der Unterschied zwischen einem ehrlichen Backtest und einem Verkaufsprospekt sind diese 4 Korrekturen.

## Selection Bias / Backtest Overfitting

Lopez de Prado et al. zeigen formal: Wenn man N Strategien testet und nur die beste meldet, ist die erwartete Maximum-Sharpe-Ratio bei **echtem Edge = 0**:

$$E[\max SR] \approx \sqrt{2 \ln N} \cdot \sigma_{SR}$$

Bei 50 Variationen und $\sigma_{SR} \approx 0.5$: Headline-Sharpe **+1.4 inflationiert**, komplett ohne echten Edge.

### Deflated Sharpe Ratio (Bailey & Lopez de Prado 2014)
Korrigiert für:
1. **Anzahl Trials** (Selection Bias)
2. **Skew & Kurtosis** der Returns (nicht-normale Verteilung)
3. **Sample-Länge** (statistische Power)

Praktisch via `mlfinlab` (Lopez de Prado's Library) oder `psr` / `dsr` Funktionen.

```python
from mlfinlab.backtest_statistics import deflated_sharpe_ratio
dsr = deflated_sharpe_ratio(observed_sr, sr_estimates,
                            number_of_trials, returns)
# Akzeptanz: DSR > 0.95 (95% Confidence)
```

## Combinatorially Symmetric Cross-Validation (CSCV)

Bailey, Borwein, Lopez de Prado, Zhu (2015): teilt Sample in **S Stücke**, bildet alle (S/2)-Untermengen als Train, Komplemente als Test. Berechnet:

**Probability of Backtest Overfitting (PBO)** = Anteil der Cases, in denen die best-in-train-Strategie out-of-sample unterdurchschnittlich abschneidet.

**Akzeptanz-Heuristik:**
| PBO | Bewertung |
|---|---|
| < 0.2 | Gute Strategie |
| 0.2 – 0.5 | Akzeptabel, vorsichtig |
| > 0.5 | **Wahrscheinlich Overfit** |

## Multiple Testing: Bonferroni & FDR

### Bonferroni (konservativ)
Bei k getesteten Strategien: akzeptiere Signifikanz nur bei
$$p < \alpha / k$$

### Holm-Bonferroni
Schrittweise, weniger konservativ.

### Benjamini-Hochberg (FDR)
Kontrolliert **False Discovery Rate** statt FWER. Praktischer für große k (z.B. Faktor-Zoo-Tests).

### Harvey/Liu/Zhu (2016)
> *"...and the Cross-Section of Expected Returns"*

Zeigen: Historische Faktor-Literatur ignoriert Multiple Testing massiv. **Realistischer Schwellwert für "neue" Faktor-t-Stat: |t| > 3.0**, nicht die übliche 2.0.

## Praktikabler Workflow (Lopez de Prado 2018)

1. **Definiere Hypothese ex ante** — vor jeglichem Datenkontakt
2. **Hold-Out gesperrt** (z.B. letzte 30 % der Daten) bis Final
3. **Walk-Forward** / Purged K-Fold-CV auf Train
4. **Bei jedem Kontakt mit Hold-Out: Trial-Counter +1, DSR-Adjustment**
5. **Logge ALLE Versuche** — auch verworfene. Einzige ehrliche Basis für Trial-Korrektur

## Andere wichtige Bias-Quellen

- **Survivorship** → vgl. [[Typische Hobby-Algo-Fehler]] §4
- **Look-ahead** → vgl. [[Typische Hobby-Algo-Fehler]] §5
- **In-Sample-Leakage** → vgl. [[Typische Hobby-Algo-Fehler]] §7
- **Selection Bias bei "Stocks in Play"**: vgl. [[Volatility Breakout - ORB]]

## Tools & Libraries

| Tool | Zweck |
|---|---|
| `mlfinlab` (Lopez de Prado) | DSR, PBO, Purged-K-Fold |
| `vectorbt` | Backtest mit eingebauter Trial-Korrektur |
| `backtesting.py` | einfach, aber **keine Trial-Korrektur** |
| `quantstats` | Performance-Reporting (inkl. DSR seit 2023) |

## Verwandte Notizen
- [[Typische Hobby-Algo-Fehler]]
- [[Realistische Erfolgsraten]]

## Quellen
- Bailey & Lopez de Prado (2014): *The Deflated Sharpe Ratio* — [PDF](https://www.davidhbailey.com/dhbpapers/deflated-sharpe.pdf)
- Bailey, Borwein, Lopez de Prado, Zhu (2015): *The Probability of Backtest Overfitting*, SSRN 2326253 — [PDF](https://www.davidhbailey.com/dhbpapers/backtest-prob.pdf)
- Harvey, Liu, Zhu (2016): *...and the Cross-Section of Expected Returns*, RFS 29(1)
- Lopez de Prado, M. (2018): *Advances in Financial Machine Learning*, Wiley

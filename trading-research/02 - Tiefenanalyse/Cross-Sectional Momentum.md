---
tags: [strategie/momentum, evidenz/stark, tiefenanalyse]
status: validiert
zeitebene: swing
markt: [equities]
evidenz: stark
quellen:
  - "Jegadeesh, Titman (1993)"
  - "Asness, Moskowitz, Pedersen (2013)"
  - "Daniel, Moskowitz (2016)"
---

# Cross-Sectional Momentum (XSMOM)

> Top-Performer kaufen, Bottom-Performer shorten. Marktneutral. Der robusteste Faktor seit 30+ Jahren.

## Funktionsweise
Sortiere ein Aktienuniversum nach vergangener Performance über einen **Formationszeitraum** (typisch 6–12 Monate, **1 Monat Skip** wegen Short-Term-Reversal). Long Top-Decile, Short Bottom-Decile, Equal-Weight oder Vola-Weight. **Marktneutral** (Dollar-/Beta-neutral).

Im Gegensatz zu [[Time-Series Momentum]]: hier zählt die **relative** Performance, nicht das absolute Vorzeichen.

## Konkrete Regeln (codierbar)

```python
# Jegadeesh/Titman (6,1,6)-Spezifikation
Universum: CRSP-listed US-Stocks
  + Filter: MarketCap > $200M, Price > $5, ADV > $1M
  
Jeden Monatsende t:
    r_form(i) = Return(i, [t-6, t-2])         # 6-Monats-Formation, 1m Skip!
    rang_i    = decile_rank(r_form across alle i)
    long_set  = top decile
    short_set = bottom decile
    pos(i)    = equal_weight oder vol_target(i)
    
Halteperiode: 6 Monate, überlappend (1/6 pro Monat rebalancen)
```

Der **1-Monats-Skip** ist kritisch — entfernt Short-Term-Reversal-Kontamination (Jegadeesh 1990).

**AMP-2013-Variante**: kombiniert Momentum mit Value (B/M) — Sharpe der Kombi deutlich höher als einzeln, da Value und Momentum negativ korreliert sind.

## Empirische Performance
- **Jegadeesh/Titman (1993):** (6,6)-Strategie: **0.95 % pro Monat, t = 3.07**, US 1965–1989. Reversal nach 12+ Monaten.
- **Asness/Moskowitz/Pedersen (2013):** Globales Value+Momentum-Portfolio über 8 Märkte: **Sharpe ~ 1.4** brutto. Momentum allein US-Stocks: Sharpe ~0.5–0.7.
- **Jegadeesh/Titman (2023, 30-Jahre-Update):** Effekt persistiert OOS, aber höhere Drawdowns nach 2000.
- **Momentum Crash 2009:** UMD-Faktor verlor in 3 Monaten ca. **−73 %**.

## Fallstricke & Overfitting-Risiken
- **Momentum Crashes** (Daniel/Moskowitz 2016): asymmetrisches Downside-Risiko in Erholungs-Phasen nach Bärenmärkten. Short-Loser-Leg rallyt aggressiv.
- **Implementations-Kosten**: Turnover ~150–250 % p.a. Frazzini/Israel/Moskowitz (2012): auf Large Caps bleibt Edge nach realistischen Kosten, auf Small Caps weniger.
- **Short-Side schwer handelbar**: Borrow-Fees auf Loser-Leg, Hard-to-Borrow für illiquide Namen.
- **Survivorship / Look-ahead**: Universum muss **Point-in-Time** sein (Delistings, historische S&P-Konstituenten).
- **Crowded Trade**: McLean & Pontiff (2016) "Does Academic Research Destroy Stock Return Predictability?" — Anomalien verlieren ~30–50 % der Stärke nach Publikation.

## Benötigte Daten/Indikatoren
- **Point-in-Time-Universum** (CRSP, Compustat, Norgate Premium Data)
- Adjusted Closes (Splits, Dividenden)
- **Delisted Stocks** inkl. Delisting-Returns (gegen Survivorship)
- Market Cap & ADV pro Tag für Filter
- Optional: Industry-Klassifikation für sektorneutrale Variante

## Verwandte Notizen
- Kategorie: [[01 - Strategie-Kategorien/Momentum]]
- Kontrast: [[Time-Series Momentum]]
- Risiken: [[06 - Risiken & Realität/Backtest Biases]]

## Quellen
- Jegadeesh & Titman (1993): *Returns to Buying Winners and Selling Losers*, JoF 48(1) — [PDF](https://www.bauer.uh.edu/rsusmel/phd/jegadeesh-titman93.pdf)
- Asness, Moskowitz, Pedersen (2013): *Value and Momentum Everywhere*, JoF 68(3) — [Wiley](https://onlinelibrary.wiley.com/doi/10.1111/jofi.12021) · [PDF](https://w4.stern.nyu.edu/facdir/lpederse/papers/ValMomEverywhere.pdf)
- Jegadeesh & Titman (2023): *Momentum: Evidence and insights 30 years later*, Pacific-Basin Finance Journal
- Daniel & Moskowitz (2016): *Momentum Crashes*, JFE 122(2)
- McLean & Pontiff (2016): *Does Academic Research Destroy Stock Return Predictability?*

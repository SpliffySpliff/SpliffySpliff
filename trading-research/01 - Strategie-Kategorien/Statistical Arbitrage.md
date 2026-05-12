---
tags: [strategie/statarb, evidenz/stark, kategorie]
status: recherche
zeitebene: [intraday, swing]
evidenz: stark
quellen:
  - "Gatev, Goetzmann, Rouwenhorst (2006)"
  - "Avellaneda, Lee (2010)"
  - "Vidyamurthy (2004)"
---

# Statistical Arbitrage (Pairs Trading, Cointegration)

> Zwei Assets, deren Linearkombination stationär ist. Trade die Abweichung vom Equilibrium-Spread.

## Grundidee
Identifiziere ein Asset-Paar (oder Korb), das gemeinsam **kointegriert** ist (Engle-Granger 1987 / Johansen 1988). Wenn der Spread `s_t = a*x_t − b*y_t` mean-reverting ist, handle die Z-Score-Extreme:
- Short Spread bei Z > +2, Long bei Z < −2
- Schließen bei Konvergenz (Z ≈ 0)

## Marktbedingungen
Liquide Aktien mit fundamentaler Verwandtschaft:
- Branche (KO/PEP, V/MA)
- Dual Listings (RDS.A/RDS.B historisch)
- ETF vs. Komponenten / NAV-Arbitrage
- ADR vs. Heimataktie

Gatev et al. dokumentierten **~11 % annualisierte Excess Returns 1962–2002**, mit deutlichem Decay nach Veröffentlichung (2003+).

## Schwächen
- **Strukturbrüche** zerstören die Beziehung (M&A, Krisen, Bilanzskandale)
- Renditen sind nach 2002 deutlich gesunken (Crowding, HFT-Konkurrenz)
- **Tail-Risk asymmetrisch**: kleine Gewinne, gelegentlich katastrophale Divergenz (LTCM 1998)
- Cointegrations-Tests in finiten Samples instabil
- Hoher Leverage nötig → Funding-Risiko
- Look-ahead Bias durch retroaktive Pair-Auswahl (siehe [[Backtest Biases]])

## Zeitebenen
Klassisch Swing (Tage–Wochen Konvergenzzeit). Moderne HFT-StatArb arbeitet intraday/sekündlich.

## Sub-Varianten
- **Distance Method** (Gatev et al. — normalisierte Preise, Sum-of-Squared-Distances)
- **Cointegration Approach** (Engle-Granger, Johansen)
- **Index Arbitrage**, ETF-vs-Basket
- **Multi-Asset Stat-Arb** (Avellaneda/Lee 2010 — PCA-basiert)
- **Merger Arbitrage / Risk Arbitrage** (verwandt, fundamentaler)

## Verwandte Notizen
- Tiefenanalyse: [[02 - Tiefenanalyse/Mean Reversion - Kurzfristig]] (Spezialfall)
- Verwandt: [[Mean Reversion]]

## Quellen
- Gatev, Goetzmann, Rouwenhorst (2006): *Pairs Trading: Performance of a Relative-Value Arbitrage Rule*, RFS 19(3) — [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=141615)
- Avellaneda, Lee (2010): *Statistical Arbitrage in the US Equities Market*, Quantitative Finance 10(7)
- Vidyamurthy, G. (2004): *Pairs Trading: Quantitative Methods and Analysis*, Wiley
- Chan, E. (2013): *Algorithmic Trading*, Wiley

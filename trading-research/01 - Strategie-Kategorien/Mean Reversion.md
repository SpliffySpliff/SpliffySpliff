---
tags: [strategie/meanreversion, evidenz/stark, kategorie]
status: recherche
zeitebene: [intraday, swing]
evidenz: stark
quellen:
  - "Poterba, Summers (1988)"
  - "De Bondt, Thaler (1985)"
  - "Chan (2013)"
---

# Mean Reversion

> Preise oszillieren um einen "fairen Wert" — nach übertriebenen Abweichungen folgt Rückkehr.

## Grundidee
Gegenpositionen zu Extrembewegungen. Quantitativ messbar über Bollinger-Bänder, RSI-Extremes, Z-Scores zu rollender Mittelung. Theoretisch fundiert durch **negative Autokorrelation auf kurzen und sehr langen Horizonten** (Poterba/Summers 1988) sowie **Liquiditätsprämien** und **Market-Maker-Inventory-Effekte** auf Intraday-Skala.

## Marktbedingungen
Funktioniert in:
- Range-bound Märkten mit geringer Volatilität ohne Trend
- Liquiden Einzelaktien auf 1–5-Tage-Horizont
- Intraday auf Mean-Reverting-Phasen (Vormittag in Index-Futures oft)

Versagt in Trendmärkten und bei Strukturbrüchen (Bankrott, M&A, Krieg, Crash).

## Schwächen
- "Catching falling knives" — asymmetrische Auszahlung: viele kleine Gewinne, gelegentlich extremer Verlust
- Hohe Transaktionskosten und Slippage relevant (viele kleine Trades)
- **Survivorship Bias** in Backtests besonders gefährlich (siehe [[06 - Risiken & Realität/Backtest Biases]])
- Strukturbrüche brechen die Mean-Reversion-Annahme

## Zeitebenen
- Intraday (Minuten–Stunden) und Swing (1–5 Tage) am stärksten
- Langfristige Mean-Reversion (Value, 3–5 Jahre) eher Faktor-Investing als Trading

## Sub-Varianten
- **Bollinger-Band-Reversal**, RSI-Extremes (Connors RSI-2)
- **Short-Term-Reversal** (Lehmann 1990, De Bondt/Thaler 1985)
- **Overnight-Reversion**, VIX-Mean-Reversion
- **Statistical Arbitrage** — siehe [[Statistical Arbitrage]]

## Verwandte Notizen
- Tiefenanalyse: [[02 - Tiefenanalyse/Mean Reversion - Kurzfristig]]
- Synthesevorschlag: [[05 - Strategievorschläge/Vorschlag B - Mean Reversion am Value Area Edge]]
- Kontrast: [[Trend Following]]

## Quellen
- Poterba, Summers (1988): *Mean Reversion in Stock Prices*, JFE 22, 27–59 — [PDF](https://economics.mit.edu/sites/default/files/publications/1-s2.0-0304405X88900219-main.pdf)
- De Bondt, Thaler (1985): *Does the Stock Market Overreact?*, Journal of Finance 40(3), 793–805
- Chan, E. (2013): *Algorithmic Trading: Winning Strategies and Their Rationale*, Wiley
- Connors, Alvarez (2009): *Short Term Trading Strategies That Work*

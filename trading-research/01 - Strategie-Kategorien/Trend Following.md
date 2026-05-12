---
tags: [strategie/trend, evidenz/stark, kategorie]
status: recherche
zeitebene: [position, swing]
evidenz: stark
quellen:
  - "Hurst, Ooi, Pedersen (2017)"
  - "Moskowitz, Ooi, Pedersen (2012)"
  - "Covel (2009)"
---

# Trend Following

> Systematisches Folgen anhaltender Preisbewegungen. Vorzeichen, nicht Niveau, ist das Signal.

## Grundidee
Kauf nach Aufwärtstrend, Short nach Abwärtstrend; Position wird gehalten, bis der Trend per Regel bricht. Typische Lookbacks: 1–12 Monate. Verzichtet bewusst auf Prognose — folgt nur dem, was schon passiert ist.

## Marktbedingungen
Funktioniert in Märkten mit anhaltender Autokorrelation in Renditen — typischerweise bei klar gerichteten Makro-Regimes (Zinszyklen, Rohstoffboom, anhaltende Risk-on/Risk-off-Phasen). Profitiert besonders in extremen Marktphasen ("crisis alpha"), weil Trends sich unter Stress verstärken. Verhaltensökonomische Begründung: initiale Unterreaktion → spätere Überreaktion (Anchoring, Herding).

## Schwächen
- Versagt in seitwärts/range-bound Märkten ("whipsaw")
- Drawdowns von 20–30 % sind historisch normal
- Hohe Sensitivität gegenüber Parameter-Wahl (Lookback, Stop-Distanz)
- Mean-Reversion auf langen Horizonten (>12 Monate) frisst Profite
- "Trend tax": 2009–2019 schwache Performance auf Aktienindizes durch QE-Glättung

## Zeitebenen
Klassisch Position-Trading (Wochen–Monate). Intraday-/Swing-Adaptionen existieren, aber empirische Evidenz ist auf mittel-/langfristigen Horizonten am stärksten.

## Sub-Varianten
- **Turtle Traders** — Donchian 20/55-Tage Breakout + ATR-Sizing (Dennis/Eckhardt 1983)
- **Time-Series Momentum** — siehe [[02 - Tiefenanalyse/Time-Series Momentum]]
- **Managed Futures / CTAs** — Dunn, Man AHL, Winton, AQR
- **Moving-Average-Crossover** — Donchian Channels, klassische MA(50)/MA(200)

## Verwandte Notizen
- Tiefenanalyse: [[02 - Tiefenanalyse/Time-Series Momentum]]
- Abgrenzung: [[Momentum]] (Cross-Sectional) vs. Time-Series
- Synthesevorschlag: [[05 - Strategievorschläge/Vorschlag A - Futures Trend + Orderflow Filter]]
- Kontrast: [[Mean Reversion]]

## Quellen
- Hurst, Ooi, Pedersen (2017): *A Century of Evidence on Trend-Following Investing*, Journal of Portfolio Management — [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2993026)
- Moskowitz, Ooi, Pedersen (2012): *Time Series Momentum*, JFE 104(2), 228–250 — [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0304405X11002613)
- Covel, M. (2009): *The Complete TurtleTrader*, HarperCollins
- Original Turtle Rules (Faith Manuskript) — [PDF](https://oxfordstrat.com/coasdfASD32/uploads/2016/01/turtle-rules.pdf)

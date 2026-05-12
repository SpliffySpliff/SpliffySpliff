---
tags: [strategie/breakout, evidenz/mittel, kategorie]
status: recherche
zeitebene: [intraday, swing, position]
evidenz: mittel
quellen:
  - "Crabel (1990)"
  - "Pardo (2008)"
  - "Aronson (2006)"
---

# Breakout-Strategien

> Eintritt, wenn der Preis ein definiertes Niveau durchbricht. Annahme: nach Konsolidierung folgt direktionale Bewegung.

## Grundidee
Ausbruch über Range-Hoch/-Tief, Konsolidierungsgrenze oder Volatilitätsschwelle. Mechanismus: **Stop-Loss-Cluster jenseits von Schlüsselniveaus** und **Trader-Aufmerksamkeit** auf Round-Numbers / Vortageshochs erzeugen kaskadenartige Folge-Orders.

## Marktbedingungen
- Volatilität expandiert nach Kompressionsphasen (Volatility-Clustering, NR7-Tage)
- Liquide Märkte mit klaren Strukturpunkten (Tageshoch, Pre-Market-Range, Opening Range)
- Häufig nach News oder am Session-Open (vgl. [[Volatility Breakout - ORB]])

## Schwächen
- **Hohe Fakeout-Rate** (oft >50 % der Breakouts)
- In Choppy-Markets systematisch verlierend
- Slippage am Breakout-Punkt teuer (alle wollen dasselbe Niveau)
- "Squeeze before squeeze" — Markt testet oft erst die Gegenseite (Stop-Hunting)
- Wird von HFT systematisch ausgebeutet

## Zeitebenen
Sehr flexibel:
- Intraday: Opening Range Breakout (ORB)
- Swing: Wochenhoch-Breakout
- Position: Donchian-55 als Trendfolge-Eintritt (Turtle-System)

## Sub-Varianten
- **Opening Range Breakout** (Crabel 1990) — siehe [[02 - Tiefenanalyse/Volatility Breakout - ORB]]
- **Donchian Channel Breakout** (Turtle System 1/2)
- **Darvas Box** (Nicolas Darvas, 1960er)
- **Volatility Breakout** (Larry Williams)
- **Bollinger Squeeze Breakout**, NR7

## Verwandte Notizen
- Tiefenanalyse: [[02 - Tiefenanalyse/Volatility Breakout - ORB]]
- Bestätigungs-Tools: [[03 - Order Flow/03 - Delta und CVD]]
- Synthesevorschlag: [[05 - Strategievorschläge/Vorschlag C - ORB mit CVD-Bestätigung]]

## Quellen
- Crabel, T. (1990): *Day Trading with Short Term Price Patterns and Opening Range Breakout*, Traders Press
- Pardo, R. (2008): *The Evaluation and Optimization of Trading Strategies*, 2nd ed., Wiley
- Aronson, D. (2006): *Evidence-Based Technical Analysis*, Wiley — kritische Diskussion mit Bootstrapping
- Zaremba, A. (2019): *Price Patterns in Commodity Futures: New Evidence*, SSRN

# Footprint Charts

## Definition
Ein Footprint Chart (auch "Cluster Chart" oder "Numbers Bars") ist eine Erweiterung der klassischen Candle. Statt nur OHLC zu zeigen, wird jede Bar in **horizontale Preis-Slots** zerlegt, in denen für jede Tick-Ebene das gehandelte Volumen aufgeschlüsselt wird. Die populärste Darstellung ist **Bid x Ask**: Links der Slot zeigt das Volumen, das am Bid (passive Verkäufer, aggressive Käufer hitten den Ask... Achtung: Konvention je nach Plattform) gehandelt wurde, rechts das Volumen am Ask. Daneben existieren Modi wie Delta, Profile, Volume-Cluster oder Volume Imbalance.

Wichtig: Die Klassifikation "wer war aggressiv?" ist eine **Inferenz**, kein Faktum. Plattformen nutzen meist eine Variante der Lee/Ready-Logik (Trade Price vs. Bid/Ask). Studien (Odders-White 2000; Ellis/Michaely/O'Hara 2000) zeigen, dass Tick-Rule/Lee-Ready ca. **78-85% korrekt** klassifizieren — Restfehler sind systematisch (Midpoint-Trades, kleine Trades, hochfrequent gehandelte Titel).

## Bid x Ask lesen
- **Diagonale Vergleichslogik**: ATAS, Sierra & Co. vergleichen Bid auf Level N mit Ask auf Level N-1 (also dem Preis darunter). Aggressive Käufer "lifteten" den Ask oben, aggressive Verkäufer "hitteten" das Bid unten.
- **Imbalance**: prozentuale Übergewichtung einer Seite (Default in ATAS 150%, profi-üblich 300-400%).
- **Delta pro Bar**: Ask-Volume − Bid-Volume; positiver Delta = Käufer-Aggression dominant.

## Typische Patterns

### P-Shape (P-förmiges Profil)
Schmaler Boden, dicker Kopf. Entsteht nach starkem Anstieg mit anschließender Konsolidierung oben. Interpretation: Short-Covering / aggressive Käufer, dann Akzeptanz oben. Häufig **am Tief eines Downtrends als Reversal-Signal** — wird aber oft als nur temporäre Stärke gewertet (Short-Squeeze, nicht Trendwende).

### b-Shape (b-förmig)
Spiegelbild: dicker Bauch unten, dünner Hals oben. Aggressive Verkäufer, danach Akzeptanz unten. Im Aufwärtstrend ein Warnsignal für Long-Liquidation.

### Stacked Imbalances
Mehrere aufeinanderfolgende Imbalances (z.B. ≥3 Buy-Imbalances bei 300%) an konsekutiven Preisebenen. Markieren oft **Support/Resistance-Zonen**: Aggression wurde "abgearbeitet", Liquidität verbraucht; das Niveau wird später häufig erneut getestet.

## Anwendungsbeispiel
ES-Future, 1-Min-Footprint: Bar bricht über Vortages-VAH aus, zeigt am Hoch 3 gestackte Buy-Imbalances (jeweils Ask:Bid > 500%), aber Close in unterer Hälfte der Bar → Verdacht auf **Absorption am Hoch** (passive Sellers haben aggressive Käufer absorbiert). Setup: Short-Bias mit Stop über High.

## Fallstricke
- **Datenfeed-Qualität entscheidend**: Aggregierter Feed (z.B. TradingView Spot-Crypto) liefert unzuverlässige Bid/Ask-Klassifikation; CME-Futures via Rithmic/CQG ist Gold-Standard.
- **Backtesting fast unmöglich**: Footprint-Patterns sind diskretionär, retrospektiv hübsch, prospektiv schwer zu validieren.
- **Survivorship-Bias in Tutorials**: Marketing-Material (ATAS-Blog, YouTube) zeigt fast nur funktionierende Setups.
- **Aktien vs. Futures**: An US-Aktien fragmentiert sich Order Flow über 16+ Venues → Footprint zeigt nur einen Ausschnitt, bei Futures (CME zentralisiert) ist das Bild vollständig.

## Quellen
- [TradingView — Volume footprint charts: a complete guide](https://www.tradingview.com/support/solutions/43000726164-volume-footprint-charts-a-complete-guide/)
- [NinjaTrader — Footprint Charts Explained: Order Flow Trading](https://ninjatrader.com/futures/blogs/ninjatrader-order-flow/)
- [Bookmap — B-Shaped and P-Shaped Market Profile](https://bookmap.com/blog/b-shaped-and-p-shaped-market-profile-how-deviations-from-balance-create-weak-highs-and-weak-lows)
- Lee, C. M. C., & Ready, M. J. (1991). "Inferring Trade Direction from Intraday Data." *Journal of Finance*, 46(2), 733–746.

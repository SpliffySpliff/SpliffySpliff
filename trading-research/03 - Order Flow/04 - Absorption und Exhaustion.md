# Absorption & Exhaustion

## Definitionen

### Absorption
Eine Partei (typischerweise institutionell) hält **große Limit-Orders** an einem Preis, die das aggressive Marktorder-Flow der Gegenseite "absorbieren". Das Preisniveau verteidigt sich gegen Aggression: trotz hohem Volumen, das in eine Richtung handelt, bewegt sich der Preis nicht (oder kaum) in diese Richtung. Absorption ist häufig — aber nicht zwingend — das Ende einer Bewegung.

### Exhaustion
Das Spiegelbild aus Sicht der Aggressoren: die treibende Seite "schießt sich aus". Aggressives Volumen bleibt hoch, doch nachfolgende Anschlussbewegung fehlt. Der Trend ist erschöpft, weil die Käufer/Verkäufer keine neue Nachfrage/Versorgung mehr finden bzw. von passiver Gegenseite gebremst werden.

Praktisch sind Absorption (Sicht des Liquiditätsanbieters) und Exhaustion (Sicht des Aggressors) **zwei Beschreibungen derselben Marktmechanik**.

## Erkennung im Footprint
- **Hoher Bid- oder Ask-Volume-Spot** an einer Preis-Ebene (z.B. 3.000 Lot ES am Bid einer einzigen Bar), **gefolgt von Preisstabilität oder Reversal**.
- **Delta divergiert vom Preis**: Bar mit stark negativem Delta, aber positivem Close (oder umgekehrt).
- **Stacked Imbalances am Extrempunkt der Bar**, die nicht zu Folge-Extension führen.
- **Lange "Wicks" mit hohem Volumen-Cluster im Wick**: Aggressive Bewegung wurde am Extrem absorbiert.

## Erkennung im Tape / DOM / Bookmap
- Auf Bookmap (Heatmap): heller (hoher) Bid- oder Ask-Cluster, der konstant gegen anflutende Market Orders steht und nicht "abgefressen" wird → klassische Wall mit Absorption-Charakter.
- **Iceberg-Detection** (Bookmap Stops & Icebergs Add-on, ATAS Open Interest-Module): Wenn an einer Ebene wiederholt Volumen abgearbeitet wird, ohne dass der sichtbare Bid kleiner wird, läuft ein Iceberg.
- Im **Time & Sales**: schnelle Reihe von Sell-Prints zu einem statischen Bid → Absorption.

## Beispiele
1. **ES 4.500-Range-Low**: Tief der Session, Footprint zeigt 4.200 Bid-Volume in der Tief-Bar, Bar schließt im oberen Drittel. Bookmap zeigt zuvor unsichtbare Liquidität am Bid (Iceberg). Long-Setup mit Stop 4 Ticks unter Tief.
2. **NQ-Trendtag-Hoch**: Vertikaler Anstieg in 15 Min, dann 5 Min Stillstand mit positivem Delta-Burst, der nicht weiter trägt. Mehrere Buy-Imbalance-Stacks am Hoch ohne Anschluss → Exhaustion. Short-Bias.
3. **Klassisches Reversal-Setup**: Aggressive Verkäufer-Welle (großer roter Footprint mit −800 Delta), aber Close grün, gefolgt von Folge-Bar grün mit Anschluss. Das Markenzeichen einer "absorption flip".

## Fallstricke
- **Survivorship-Bias**: Erfolgreiche Absorptions werden im Nachhinein gefeiert. In Wahrheit gibt es viele "Pseudo-Absorptionen", in denen Preis kurz hält, dann doch durchbricht (Liquidität war nur temporär).
- **Iceberg-Camouflage**: Was wie Absorption aussieht, ist ggf. nur ein Iceberg-Hedger ohne Reversal-Absicht. Er füllt Auftrag ab; sobald gefüllt, ist der "Support" weg.
- **Zeitliche Asymmetrie**: Echte Absorption setzt voraus, dass die passive Seite **wirklich verteidigt**. Algos können Volumen absorbieren, danach wegziehen, ohne dass Reversal kommt.
- **Markt-Mikrostruktur-Effekte**: An ETF-Spot oder fragmentierten Aktien kann sichtbarer DOM-Druck **ein Bruchteil** des realen Volumens sein. Dark Pools, Hidden Orders, RFQ verzerren.
- **Trader Edutainment**: "Smart Money Absorption" ist ein häufig benutzter, schwammig definierter Begriff. Ohne quantitative Validierung sollte man diskretionäre Absorption-Trades nicht overhypen.

## Quellen
- [Bookmap — How to Read and Trade Iceberg Orders](https://bookmap.com/blog/how-to-read-and-trade-iceberg-orders-hidden-liquidity-in-plain-sight)
- [Bookmap — Detecting Stop Runs Using CVD & Iceberg Absorption](https://bookmap.com/blog/detecting-stop-runs-using-cvd-and-iceberg-absorption-for-strategic-trading)
- [NinjaTrader — Footprint Charts Explained](https://ninjatrader.com/futures/blogs/ninjatrader-order-flow/)

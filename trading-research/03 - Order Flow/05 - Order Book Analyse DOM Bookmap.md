# Order Book Analyse (DOM, Bookmap)

## Definition
Die **Depth-of-Market (DOM)** Analyse betrachtet das **limit order book**: Stack aller offenen Limit-Orders auf der Bid- und Ask-Seite, gestaffelt nach Preisebene. Übliche Datentiefen:
- **CME Globex Futures**: 10 Levels (MBP-10) bzw. Market-by-Order (MBO) seit 2017.
- **CME-Optionen**: 3 Levels.
- **Aktien**: variabel je Venue; Nasdaq TotalView geht volle Tiefe.

**Bookmap** visualisiert nicht die DOM-Tabelle, sondern eine **2D-Heatmap** (X-Achse Zeit, Y-Achse Preis, Farbintensität = Order-Größe am Level). Dadurch werden zeitliche Veränderungen — angesetzte und gepullte Liquidität — sichtbar, was die statische DOM nicht leisten kann.

## Iceberg-Detection
Ein **Iceberg** ist eine Limit-Order, die nur einen Teil ihrer Größe sichtbar an die Börse stellt; der Rest wird nachgenährt, sobald die sichtbare Tranche gefüllt ist.

**Detektion**:
- Volumen wird wiederholt an einer Preis-Ebene gehandelt, **ohne dass die sichtbare Bid/Ask-Tiefe abnimmt** (oder sie wird sekundenschnell nachgefüllt).
- Bookmap's "Stops & Icebergs"-Add-on flaggt erkannte Icebergs automatisch.
- Auf MBO-Daten (Rithmic, CME MBO direkt) sind individuelle Orders mit ID trackbar — Iceberg-Refills hinterlassen Spuren.

CME-MBO ist hierfür Gold-Standard, weil jede Order eine eindeutige ID hat und Refill-Patterns sichtbar werden.

## Spoofing
**Spoofing** = Aufgabe nicht-ernsthafter Orders mit Cancel-Absicht, um andere Marktteilnehmer zu täuschen. Nach **Dodd-Frank Act (2010)** in den USA illegal.

**Erkennung im Heatmap**:
- Plötzlich erscheinende große Walls, die kurz vor Erreichen verschwinden (kein Fill).
- Wiederholte Add/Cancel-Muster auf bestimmten Levels.
- Bekanntester Fall: **Navinder Sarao** ("Flash Crash 2010"), nutzte 188- und 289-Lot-Spoofing-Layering im ES-Future, ca. $200M nominal, Orders 19.000-mal modifiziert.

Spoofing-Erkennung ist visuell auf Bookmap möglich, aber forensisch nur mit MBO-Daten zweifelsfrei nachweisbar.

## Liquiditäts-Heatmaps
Heatmap-Anwendungen:
- **Liquidity Magnets**: dichte Cluster ziehen Preis oft an (Stop-Hunts, Market-Order-Sweeps).
- **Liquidity Voids**: schwache Tiefe = potenzielle schnelle Bewegung bei Reaktion.
- **Walls als Support/Resistance**: große, stabile Limit-Order — solange sie steht, Hindernis; sobald sie weggezogen wird, Signal für Richtungswechsel ("ghosting").

## Praktisches Beispiel
NQ-Future kurz vor FOMC: Bookmap zeigt 800-Lot-Bid auf 18.520, 50 Ticks unter Spot. Während Statement-Veröffentlichung saugt Markt nach unten, Bid bleibt sichtbar bis exakt 18.521 stehen, wird dann gepullt — klassisches **Bait-Wall** / Pull-Spoof. Preis bricht auf 18.495 durch, weil keine echte Verteidigung lag.

## Limitationen
- **Latenz**: Retail-Feeds (auch dxFeed, IQFeed) haben Snapshot-Frequenzen von 50ms-200ms. Echte HFT-Algorithmen sehen Microsekunden-Granularität. Was du auf Bookmap siehst, ist **immer zeitlich zurückliegend**.
- **Hidden Orders**: Iceberg-Anteile, Reserve Orders, Dark Pool Routing — **alles unsichtbar** im DOM. Bei Aktien (NYSE, Nasdaq) ist Off-Exchange-Volumen ca. 40-50% des Gesamtvolumens (FINRA TRF). Bei Futures CME ist es nahe 100% transparent, deshalb sind Futures die einzig sinnvolle Heatmap-Spielwiese.
- **Spoofing & Layering**: Selbst wenn illegal, kommt es vor. Das, was du siehst, ist nicht zwingend echte Absicht.
- **Order Book ≠ Trade Intent**: Eine Wall heißt nicht, dass dort gekauft wird — nur dass jemand bereit ist, **falls Preis kommt**. Sie kann jederzeit gezogen werden (Sub-Sekunde).
- **Marketing vs. Realität**: Bookmap-Marketing suggeriert "Edge durch Liquiditätsvisualisierung". Tatsächlich nutzen die größten algorithmischen Spieler genau diese Visualisierungen nicht — sie haben proprietäre Co-Location-Feeds. Retail bekommt verzögerte und teils manipulierte Sicht.

## Quellen
- [CME Group — Market by Order (MBO)](https://www.cmegroup.com/education/market-by-order-mbo.html)
- [Bookmap — Iceberg Orders Tracker](https://bookmap.com/knowledgebase/docs/KB-Bookmap-Wiki-Iceberg-Orders-Tracker)
- [Wikipedia — Spoofing (finance) / Dodd-Frank §747](https://en.wikipedia.org/wiki/Spoofing_(finance))
- Bookstaber, R. (2007). *A Demon of Our Own Design.* Wiley. — Hintergrund zu Marktstruktur, Komplexität und versteckter Liquidität.

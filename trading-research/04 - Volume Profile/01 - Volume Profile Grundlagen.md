# Volume Profile Grundlagen

## Definition
Ein **Volume Profile** ist ein Histogramm, das das gehandelte Volumen **horizontal über Preisebenen** verteilt — anders als das übliche Volumen-Balkendiagramm, das Volumen pro Zeitintervall darstellt. Die Y-Achse ist Preis, die X-Achse ist Volumen. Daraus liest man **Wo** der Markt am meisten gehandelt hat, nicht **Wann**.

Die zugrundeliegende Idee stammt aus J. Peter Steidlmayers **Market Profile** der 1980er-Jahre (CBOT), wurde aber von TPO-Counting auf echtes Volumen übertragen, sobald elektronische Daten verfügbar waren.

## Drei Hauptvarianten

### VPVR — Volume Profile Visible Range
Berechnet das Profil ausschließlich aus den **aktuell sichtbaren Bars** im Chart-Viewport. Zoomt man heraus, ändern sich VAH/VAL/POC. Vorteil: dynamisch und kontextuell. Nachteil: Werte sind chart-abhängig, nicht reproduzierbar.

### Session-Profile (auch: Periodic / Fixed Range Profile)
Wird pro **definierter Periode** berechnet — Day, Week, Month, Session (RTH vs. ETH bei US-Futures). Liefert reproduzierbare, festgenagelte POC/VAH/VAL pro Periode. Typischer Anwendungsfall: tägliche RTH-POCs/VAs als Referenz-Level für die Folgesession.

### Composite Profile
**Mehrere Sessions zusammengefasst** zu einem Mega-Profile — z.B. Wochen-, Monats-, Multi-Jahres-Composites. Identifiziert übergreifende Akzeptanzzonen ("acceptance areas") und Single Prints / Low Volume Nodes (LVN) auf höherer Zeitebene. Dalton ("Markets in Profile") nutzt Composites extensiv für Swing-Kontext.

## Lesart von Profil-Shapes
- **Normal Distribution / D-Shape**: glockenförmig, gut akzeptiertes Value-Area; Markt in Balance.
- **P-Shape**: Long-Body oben, dünnes Tail unten — typisch nach Short-Cover-Rally.
- **b-Shape**: Long-Body unten, dünnes Tail oben — typisch nach Long-Liquidation.
- **Double Distribution**: zwei Glocken übereinander — Markt hat zwei Wertbereiche gefunden (z.B. Pre-/Post-News).
- **Trending Profile**: dünn, kein klarer POC — direktional, kein Akzeptanz-Auftrag.

## Praktisches Beispiel
ES-Future, Daily-Volume-Profile vom Vortag zeigt POC bei 5.230, VAH 5.245, VAL 5.215. Bei Open des nächsten Tages liegt Preis 5.218 (innerhalb der VA). Erwartung nach Auction Market Theory: Rotation Richtung POC. Setup: Long mit Ziel POC, Stop unter VAL.

## Was Volume Profile NICHT ist
- Es ist **kein Indikator für Aggression** (Käufer vs. Verkäufer). Dafür braucht es Footprint/Delta. Volume Profile zählt nur **Brutto-Volumen pro Preis**, ohne Richtungs-Information.
- Es ist **keine zeitliche Sequenz** — das ursprüngliche Market Profile/TPO hat die Zeit-Dimension (Letters), klassisches Volume Profile aggregiert die Zeit weg.
- Es ist **kein magischer Hebel**: Volume Profile zeigt historische Akzeptanz, nicht zukünftige Preisbewegung. Edge entsteht durch Kombination mit Kontext (Open Type, News, Trend).

## Fallstricke
- **Visible-Range-Falle**: Im VPVR-Modus ändert sich der POC, wenn du den Chart-Zoom änderst. Trade-Levels bitte aus **festen Sessions** ableiten, nicht aus zufälligem Viewport.
- **Tick-Größen-Bias**: Auf Tick-Größen-aggregierten Profilen sieht ein POC anders aus als auf groberem Binning. Konventionen beachten (z.B. ES = 0,25 Punkt-Bins).
- **Aktien-Fragmentierung**: Volume Profile an einer einzigen Venue (z.B. NYSE) ist unvollständig. SIP-konsolidierte Daten oder Bloomberg/Refinitiv verwenden.
- **Edutainment-Hype**: "POC ist Magnet" ist eine plausible Faustregel, **keine statistisch validierte Wahrheit**. Es gibt keine peer-reviewed Studie, die einen quantifizierbaren Edge aus reinem POC-Trading belegt.

## Quellen
- [TradingView — Volume profile indicators: basic concepts](https://www.tradingview.com/support/solutions/43000502040-volume-profile-indicators-basic-concepts/)
- [ATAS — Volume Profile Types](https://atas.net/atas-possibilities/indicators/volume-profile-types/)
- Steidlmayer, J. P., & Hawkins, S. B. (2003). *Steidlmayer on Markets: Trading with Market Profile* (2nd ed.). Wiley.

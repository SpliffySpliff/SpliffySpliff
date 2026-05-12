# Market Profile (Steidlmayer / TPO)

## Definition
Das **Market Profile** ist die Ur-Form aller Volumen-basierten Akzeptanz-Konzepte. Entwickelt 1984-85 von **J. Peter Steidlmayer** (Trader am CBOT) mit Kevin Koy als Visualisierungs-Tool für CBOT-Members. Statt Volumen wird **Zeit pro Preis** gezählt — die **Time-Price Opportunity (TPO)**.

Jede 30-Min-Periode bekommt einen **Buchstaben** (A, B, C, ...). Pro Preisebene, an der in dieser Periode gehandelt wurde, wird der Buchstabe seitlich auf der Y-Achse abgedruckt. Das Ergebnis ist eine **horizontale Verteilung der Markt-Beobachtungszeit**.

## Unterschied zu Volume Profile

| Aspekt | Market Profile (TPO) | Volume Profile |
|---|---|---|
| Misst | Zeit pro Preis (Bracket-Letter-Count) | Volumen pro Preis |
| Quelle | CBOT 1985 (Steidlmayer) | Spätere Adaption, sobald elektronische Volumen-Daten verfügbar |
| Aussage | Wie lange war Preis dort akzeptiert | Wie viel Größe hat dort gehandelt |
| Vorteil | unabhängig von Volumen-Spikes (z.B. Single-Trade-Größe) | quantitativ präziser |
| Nachteil | Single Print pro Bracket zählt gleich wie 10.000 Lots | Volumen-Spikes (Stops, Algos) können Profile verzerren |

Beide ergänzen sich; viele Pros nutzen **beide overlay**.

## Schlüssel-Konzepte

### Initial Balance (IB)
Range der **ersten zwei 30-Min-Brackets** (also erste Stunde Trading, Bracket A + B). Diese Range definiert oft den **Tages-Spielraum**:
- **IB-Extension** in nur eine Richtung → Trendtag.
- **Range innerhalb IB** → Balanced Day.
- Daltons "Range Extension"-Heuristiken: Wenn Preis IB um mehr als 50% nach einer Seite extended, ist die andere Seite OTF-(Other Timeframe)-Schwach.

### Single Prints
Preisebenen, die nur **von einem einzigen Bracket-Letter** berührt wurden. Indikator für **schnelle, "unfertige" Bewegung**, in der wenig Akzeptanz stattfand. Gilt als **High-Probability-Return-Target**: Markt kehrt häufig zurück, um diese Lücke auszufüllen ("unfinished business").

### Poor Highs / Poor Lows
Extremes Hoch/Tief ohne Ausschluss-Tail (also nur ein einziger TPO am Extrem) → "poor", weil keine echte Ablehnung. Häufiges Retest-Ziel.

### Day Types (Dalton)
- **Normal Day**: IB groß, Range bleibt drin.
- **Normal Variation Day**: leichte IB-Extension.
- **Trend Day**: starke direktionale Extension in eine Richtung.
- **Double-Distribution Trend Day**: zwei klare Wertbereiche während eines Trends.
- **Non-Trend Day**: schmal, illiquid.

### Open Types (Dalton)
Wichtige Signal für die erwartete Day-Type-Wahrscheinlichkeit:

1. **Open-Drive**: Eröffnung mit aggressivem Push in eine Richtung — höchste Konfidenz, OTF entschieden. Häufiger Trend-Tag.
2. **Open-Test-Drive**: Eröffnung testet bekanntes Level, kehrt um, dann Drive in andere Richtung.
3. **Open-Rejection-Reverse**: Push, dann Reversal durch Open-Preis → geringere Konfidenz, ~50% Hit-Rate für Extrem-Halt.
4. **Open-Auction (Inside Value/Range)**: Eröffnung innerhalb Vortages-Value, Rotation — geringste Konfidenz, oft Bilanztag.
5. **Open-Auction (Out of Range)**: Eröffnung außerhalb, höhere direktionale Wahrscheinlichkeit.

## Beispiel
ES Open bei 5.430, vor RTH-Range war 5.420-5.435. Bracket A bricht in den ersten 30 Min nach oben auf 5.445 (klare Direktion), B-Bracket extended weiter, kein Pullback in die A-Range → **Open-Drive**. Erwartung: Trend Day. Setup: jeder Pullback in Bracket-Lows wird gekauft, Stop unter IB Low.

## Hauptquelle
**Dalton et al., *Mind Over Markets* (1993)** ist die definitive Anwender-Bibel. *Markets in Profile* (Dalton, 2007) ergänzt den Composite/Swing-Kontext. Steidlmayer selbst hat *Steidlmayer on Markets* (2nd ed. 2003) geschrieben, das aber stärker theoretisch-philosophisch ist.

## Fallstricke
- **Bracket-Zeit 30 Min ist Konvention** vom CBOT-Pit-Trading. Auf 24h-Globex-Märkten künstlich. Manche nutzen RTH-only Profile, andere ETH-inklusive.
- **TPO-Count vs. Volumen-Aggression** kann auseinanderlaufen: ein langer Tail mit 6 Brackets, aber niedrigem Volumen ist anders zu lesen als 1 Bracket mit massivem Volumen.
- **Dalton-Begriffe ("OTF", "Other Timeframe Buyer")** sind interpretativ, schwer quantifizierbar. Es ist eine **Narrative-Framework**, kein deterministischer Indikator.
- **Empirie dünn**: Akademisch validierte Edge-Statistiken zu Open-Types sind rar; das Wissen ist tradiertes Floor-Trading-Know-how. ParaCurve und WindoTrader haben Hit-Rate-Statistiken zu einzelnen Open-Types publiziert (z.B. Open-Drive ~70% Trend-Day-Wahrscheinlichkeit), aber methodisch nicht peer-reviewed.

## Quellen
- Dalton, J. F., Jones, E. T., & Dalton, R. B. (1993). *Mind Over Markets.* Probus Publishing.
- Dalton, J. F. (2007). *Markets in Profile.* Wiley.
- Steidlmayer, J. P., & Hawkins, S. B. (2003). *Steidlmayer on Markets: Trading with Market Profile* (2nd ed.). Wiley.
- [ATAS — Analyzing TPO: 5 important elements in Jim Dalton's opinion](https://atas.net/volume-analysis/analyzing-tpo-5-important-elements-in-jim-daltons-opinion/)
- [ParaCurve — Day Opening Types as a Precursor](https://paracurve.com/2020/02/day-opening-types.html)

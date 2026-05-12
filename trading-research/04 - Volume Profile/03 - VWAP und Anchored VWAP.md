# VWAP & Anchored VWAP

## Definition

### VWAP (Volume Weighted Average Price)
$$\text{VWAP} = \frac{\sum (P_i \cdot V_i)}{\sum V_i}$$

Über alle Trades $i$ einer Periode (typischerweise Tradingtag). Eingeführt 1988 von **Berkowitz, Logue & Noser** in *The Total Cost of Transactions on the NYSE* (Journal of Finance) als institutioneller Execution-Benchmark.

### Anchored VWAP (AVWAP)
Identische Berechnung, **gestartet an einem manuell gewählten Ankerpunkt** (Earnings-Datum, IPO, FOMC-Statement, Swing-High, etc.). Brian Shannon (Alphatrends) popularisierte AVWAP seit 2002 und veröffentlichte 2022 *Maximum Trading Gains With Anchored VWAP* (CMT Association).

## Institutionelle Bedeutung
- VWAP ist der **Standard-Benchmark für Execution-Algos** bei Buy-Side-Firmen. Ein Broker, der "VWAP-fills" abliefert, hat den Auftrag im Average der Session-Liquidität ausgeführt.
- Asset Manager skalieren große Orders über den Tag, um VWAP zu treffen → erzeugt **strukturelle Order-Flow-Aktivität rund um VWAP**.
- Folge: Preis interagiert oft mit VWAP, weil dort algorithmische Execution stattfindet. Das ist **keine Magie** — es ist eine Reflexion echter Auftrags-Routing-Mechanik.

## Standardabweichungs-Bänder
Erweiterung mit ±1σ, ±2σ, ±3σ (volumengewichtet berechnet). Funktion ähnlich Bollinger Bands, aber auf Trades, nicht Schlusspreisen.

- **±1σ ≈ 68% Akzeptanz** — typische "fair-value-Range".
- **±2σ ≈ 95%** — Extrem-Reversion-Zone.
- **±3σ** — selten getroffen; oft mit News/Tail-Events korreliert.

Brian Shannon empfiehlt zudem **fibonacci-inspirierte Bänder** (1, 1.618, 2.618σ).

## Anchoring-Strategien (nach Shannon)

1. **Earnings AVWAP**: vom letzten Earnings-Print verankert. Zeigt durchschnittliche Position aller Käufer seit letzten Zahlen. Häufige Reaktionszone bei Re-Tests.
2. **Swing-High / Swing-Low AVWAP**: vom letzten signifikanten Top/Boden. Hält sich Preis darüber → Bullen kontrollieren.
3. **Event AVWAP**: FOMC, CPI, Geo-Politik. Macht den "Vor-Event vs. Nach-Event"-Preis sichtbar.
4. **YTD- / Multi-Year-AVWAP**: für Position-Trader; entspricht einem composite institutional cost basis.
5. **Inverse Anchoring**: vom letzten Hoch nach unten anchoren — funktioniert symmetrisch für Bär-Setups.

## Beispiel
Stock XYZ veröffentlicht starke Earnings, Gap +8%. AVWAP von Earnings-Tag verankert. In den folgenden 6 Wochen drifted Preis seitwärts, Pullback erreicht AVWAP exakt am 36. Tag → Reaktionsbar mit hohem Volumen. Setup: Long mit Stop unter AVWAP-Bar, Ziel vorheriges Earnings-Hoch.

## Fallstricke
- **VWAP ist intraday eine bewegliche Zielscheibe**: Frühmorgens stark volatil, weil wenig Volumen die Berechnung dominiert. Erste 30 Min oft unbrauchbar.
- **Tag/Tag Reset**: Standard-VWAP setzt täglich zurück. Wer VWAP-Strategien über Multi-Day-Holds nutzt, braucht zwingend Anchored-Variante.
- **VWAP ≠ Edge**: VWAP funktioniert, weil Algos darauf routen — aber **alle wissen das**. Naive "Buy below VWAP / Sell above" funktioniert nicht ohne Trend-/Kontext-Filter.
- **Aktien-Fragmentierung**: VWAP einer einzelnen Venue (NYSE only) ≠ konsolidierter VWAP (SIP). Algos rechnen typischerweise mit SIP-VWAP. Retail-Tools zeigen oft nur Primary-Venue.
- **Anchor-Auswahl ist subjektiv**: Mit hinreichend vielen möglichen Ankerpunkten findet man retrospektiv immer einen, der "perfekt passt". Survivorship-Bias!
- **Konfundierung mit Pivots/MA**: Oft fallen VWAP, gleitende Durchschnitte und Pivots zusammen. Welcher Faktor das Reaktions-Niveau wirklich erzeugt, ist nicht trennscharf identifizierbar.

## Quellen
- Berkowitz, S. A., Logue, D. E., & Noser, E. A. (1988). "The Total Cost of Transactions on the NYSE." *Journal of Finance*, 43(1), 97-112.
- Shannon, B. (2022). *Maximum Trading Gains With Anchored VWAP: The Perfect Combination of Price, Time & Volume.* — siehe [CMT Association Paper](https://cmtassociation.org/wp-content/uploads/2024/01/Shannon-Specific-Anchored-VWAP-Strategies-1.pdf)
- [StockCharts ChartSchool — Anchored VWAP](https://chartschool.stockcharts.com/table-of-contents/technical-indicators-and-overlays/technical-overlays/anchored-vwap)
- [Wikipedia — Volume-weighted average price](https://en.wikipedia.org/wiki/Volume-weighted_average_price)

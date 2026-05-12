# POC, Value Area, VAH/VAL

## Definitionen

### Point of Control (POC)
Der Preis mit dem **höchsten Volumen-Eintrag** im betrachteten Profil. Wird oft als "fair price" oder "Magnet" bezeichnet, weil die Mehrheit der Marktteilnehmer dort gehandelt hat. Bei einer Session entspricht der POC dem Preis größter Akzeptanz.

### Value Area (VA)
Preisbereich, in dem **70% des Volumens** stattgefunden haben. Dies basiert auf Steidlmayers Annahme, dass der Markt ein quasi-Normalverteilungs-Profil bildet, bei dem **±1 Standardabweichung ca. 68,2%** abdeckt — gerundet auf 70%.

> Wichtige Einschränkung: empirisch sind Volumen-Profile **selten echte Normalverteilungen**. Sie sind häufig multimodal (Double Distribution) oder schief (P/b). Die 70%-Regel ist eine **operationale Konvention**, kein statistisches Gesetz.

### VAH / VAL
- **VAH** (Value Area High): obere Grenze der 70%-Zone.
- **VAL** (Value Area Low): untere Grenze.

Die Berechnung beginnt am POC und expandiert nach oben/unten zu dem Preis mit dem nächsthöheren Volumen, bis 70% abgedeckt sind.

## Steidlmayer / Auer Background
J. Peter Steidlmayer, Trader am Chicago Board of Trade, entwickelte ab Mitte der 1970er Jahre **Market Profile / TPO** und führte es 1984-85 mit Kevin Koy als CBOT-Educational-Produkt ein. Die zentrale Idee: der Markt sucht durch Auktion **Wert (value)**, definiert als die 70%-Zone, in der Käufer und Verkäufer übereinstimmen. **James Dalton** popularisierte das Framework mit *Mind Over Markets* (1993) und *Markets in Profile* (2007).

## Praktische Anwendung

### Value-Area-Rule (Dalton)
Wenn der Markt **above the prior day's Value Area opens**, und der erste Test der Value Area **fehlschlägt** (kein Re-Entry), dann hat die Eröffnung eine direktionale Tendenz nach oben. Spiegelbildlich für unten. Die genaue Regel: "80% rule" — wenn Preis zurück in die VA kommt und dort **2 konsekutive 30-Min-TPOs** hält, hat die Re-Entry eine ~80% Wahrscheinlichkeit, die ganze VA durchzulaufen (vom Hörensagen tradiert, mehrere Backtests zeigen geringere Hit-Rates).

### POC als Magnet
Wenn der Preis sich von POC entfernt, neigt er erfahrungsgemäß zur Rückkehr (Mean Reversion). Allerdings: dieser "Magnet"-Effekt ist **kontextabhängig** (range vs. trend day). An Trend-Tagen wird POC oft nie wieder getestet.

### Naked POC
POC einer Vor-Session, der **nie wieder getestet wurde** ("naked"). Gilt als latentes Magnet-Level. Auch hier: erfahrungsbasiert, keine streng-statistische Bestätigung.

## Beispiel
NQ-Future Vor-RTH-Profile: POC 16.420, VAH 16.460, VAL 16.380. RTH-Open bei 16.470 (über VAH). Erste Stunde testet 16.460 von oben, hält → bullische Auktion. Setup: Long mit Stop unter VAH 16.455, Ziel naked POC der Vor-Vorwoche bei 16.510.

## Fallstricke
- **70% ist Konvention, nicht Naturgesetz**. Manche Trader nutzen 68%, 75% oder 80%. Konsistenz im Setup wichtiger als das exakte Prozent.
- **POC-Migration**: Während einer Session wandert der POC mit jeder neuen Trade. Erst nach Session-Close ist der "finale POC" festgestellt — Intraday-Werte sind volatil.
- **Niedrig-Volumen-Sessions** (Feiertage, Halbtage) liefern POCs/VAs mit geringer statistischer Aussagekraft.
- **POC-Reverenz im aufwendigen Trend** versagt regelmäßig. Trendtage haben P/b-Profile und der "Magnet"-Effekt funktioniert nicht.
- **Empirische Validierung dünn**: Akademische Studien zur Profit-Faktor-Statistik von POC/VA-Trades sind selten. Das Framework lebt stark aus der **Tradition und der Logik der Auction Market Theory**, nicht aus reproduzierbaren Backtests.

## Quellen
- [Wikipedia — Market profile](https://en.wikipedia.org/wiki/Market_profile)
- Dalton, J. F., Jones, E. T., & Dalton, R. B. (1993). *Mind Over Markets: Power Trading with Market Generated Information.* Probus Publishing.
- Dalton, J. F. (2007). *Markets in Profile: Profiting from the Auction Process.* Wiley.
- [GoodCrypto — Ultimate Guide to Volume Profile: VPVR, VPSV & VPFR](https://goodcrypto.app/ultimate-guide-to-volume-profile-vpvr-vpsv-vpfr-explained/)

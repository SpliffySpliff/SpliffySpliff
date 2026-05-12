# Kombinierte Anwendung von Volume Profile

## Grundprinzip
Volume Profile als **eigenständige Strategie funktioniert nicht zuverlässig**. POC, VAH, VAL sind statische Levels — sie sagen nichts über Trendkontext, News-Drift oder zukünftige Liquidität. Profis nutzen Profile **als Referenzlandkarte**, auf der dann Trend-, Breakout-, oder Order-Flow-Logiken angesetzt werden.

Im Kern gelten zwei Marktzustände aus der Auction Market Theory (Dalton/Steidlmayer):
- **Balance**: Markt in Wert; Range-Bound; **Mean-Reversion-Trades** Richtung POC dominieren.
- **Imbalance / Trend**: Markt sucht Wert; direktional; **Breakout/Trend-Continuation-Trades** dominieren.

Die Edge entsteht daraus, **den aktuellen Zustand zu identifizieren** und das passende Setup zu wählen — nicht aus dem Profil allein.

## Klassische Kombinations-Setups

### 1. Failed Breakout über VAH (Fade)
**Setup**: Markt eröffnet innerhalb der Vortages-VA. Preis steigt über VAH, jedoch:
- **Footprint zeigt keine Buy-Aggression** (Delta flach oder negativ trotz steigendem Preis).
- **CVD divergiert**.
- Preis bricht binnen 1-2 Bars zurück unter VAH.

**Trade**: Short bei Re-Entry in VA, Stop über Wick-High, Ziel POC bzw. VAL.

**Logik**: Breakout ohne Aggression = Liquiditätssweep / Stop-Run. Aktien-/Futures-Pros nutzen genau diese Falle, um Retail-Breakout-Trader zu liquidieren.

### 2. Open-Drive über Vortages-VAH (Trend Following)
**Setup**: Eröffnung über VAH, Bracket A extended weiter, **Footprint zeigt klare Buy-Imbalance-Stacks**, CVD trendkonform.

**Trade**: Buy First Pullback to VAH (jetzt Support), Stop unter VAH-Volume-Cluster, Trailing-Stop entlang Bracket-Lows.

**Logik**: Echte Initiative durch OTF-Buyer; Vortages-VAH ist als Akzeptanz-Floor genutzt.

### 3. POC-Magnet im Balance-Tag
**Setup**: Open-Auction inside Vortages-VA, kein direktionaler Drive, IB schmal.

**Trade**: Fade Extremes; Long am VAL mit Ziel POC, Short an VAH mit Ziel POC.

**Logik**: Markt rotiert in Balance um Wert; mean reversion. Voraussetzung ist, dass der Open-Type tatsächlich Balance signalisiert.

### 4. Naked POC Re-Test
**Setup**: Composite-Profile zeigt einen unbearbeiteten POC der letzten 5-10 Sessions. Preis nähert sich.

**Trade**: Anticipation-Trade Long/Short in Richtung POC, dann Reaktions-Setup am POC selbst (Reaktion oder Durchbruch).

**Logik**: Unfinished business / Akzeptanz-Magneten. Empirisch beobachtet, aber nicht streng quantifiziert.

### 5. Anchored VWAP + Volume Profile Confluence
**Setup**: Anchored VWAP von letzter Earnings/News-Event fällt auf vorigen POC zusammen.

**Trade**: Reaktions-Setup an dieser Confluence — Long bei Bull-Order-Flow-Bestätigung, Short bei Bear-Bestätigung.

**Logik**: Zwei unabhängige Akzeptanz-Metriken überlagern sich; höhere statistische Robustheit als jedes Level für sich. Brian Shannon's Hauptthese.

### 6. Single Print Return
**Setup**: Vortages-Profile hat klar identifizierbares Single-Print-Gap zwischen 5.230-5.236. Preis nähert sich von oben.

**Trade**: Erwarte Reaktion entweder bei Eintritt ins Gap (Bounce) oder Fill (mean reversion). Setup ist diskretionär nach Order-Flow-Bestätigung.

**Logik**: Single Prints repräsentieren unfertige Auktion. Häufige Re-Test-Wahrscheinlichkeit, in Praxis ~60-70% innerhalb einer Woche (anekdotisch, nicht peer-reviewed).

## Kritische Bewertung
- **Edutainment-Marketing** behauptet oft, Volume Profile sei "der heilige Gral". Es ist es nicht. Es ist eine **Karte** — die Edge liegt im **Wann und Wie** du sie liest.
- Echte Edge-Statistiken: Es gibt **keine** peer-reviewed Studie, die einen positiven Sharpe für reines POC-/VA-Trading belegt. Hit-Rate-Behauptungen aus Trading-Education sind selten methodisch sauber.
- **Confluence ≠ Magie**: Mehrere Levels überlagern sich oft "zufällig". Aussagekräftig ist Confluence nur, wenn die einzelnen Levels **unabhängig motivierte Reaktionspunkte** sind.
- **Trend overrides Profile**: An echten Trend-Days (Open-Drive, gleitende Trends) wird POC oft den ganzen Tag nicht mehr getestet. Wer dort POC-Magnet handelt, verliert.

## Fallstricke
- **Backtesting**: Diskretionäre Setups sind schwer zu backtesten. Wer Volume Profile nutzt, sollte **rigoroses Journaling** (Setup-Type, Hit-Rate, Reward/Risk) führen, um eigene Edge empirisch zu validieren.
- **Confirmation Bias**: Bei genug Levels (VAH, VAL, POC, Naked POC, Single Print, IB-High, IB-Low, AVWAP, ...) findet man retrospektiv immer ein Erklärungs-Level. Vorab-Definition ist Pflicht.
- **Markt-Regime-Wechsel**: Was im Range-Bound-ES funktioniert, scheitert im trendenden NQ während Earnings-Season. Regime-Awareness ist kein Bonus, sondern Voraussetzung.

## Quellen
- Dalton, J. F. (2007). *Markets in Profile: Profiting from the Auction Process.* Wiley.
- [TrendSpider — Volume Profile Trading Strategies](https://trendspider.com/learning-center/volume-profile-strategies/)
- [FTMO — Master Volume Profile Trading with the VA Breakout Strategy](https://ftmo.com/en/blog/master-volume-profile-trading-with-the-va-breakout-strategy/)
- Shannon, B. (2022). *Maximum Trading Gains With Anchored VWAP.*

# Delta & Cumulative Volume Delta (CVD)

## Definition
**Delta** = Ask-Volume − Bid-Volume innerhalb einer Bar (oder eines Zeitfensters). Positiver Delta deutet auf Käufer-Aggression hin, negativer auf Verkäufer-Aggression. Wie immer bei Order-Flow-Metriken: die Zuordnung "aggressiv" basiert auf einer Klassifikationsheuristik (Trade-Preis relativ zu Bid/Ask, Tick-Rule etc.) — bei aggregierten Aktien-Feeds und Crypto-Spot oft fehleranfällig.

**Cumulative Volume Delta (CVD)** ist die laufende Summe aller Deltas über eine gewählte Periode (Session, Anchored-Range). CVD zeichnet eine Linie, deren Steigung die kumulative Käufer/Verkäufer-Bilanz zeigt — sie ist analog zur OBV (On-Balance Volume), aber präziser auf aggressive Volumina fokussiert statt auf Up/Down-Bar-Logik.

## Lesart
- **CVD steigt synchron mit Preis** → trendkonform: Aggressoren treiben.
- **CVD flach bei steigendem Preis** → Preis steigt ohne Aggression, getragen von Sell-Limit-Liquidität, die zurückgezogen wird, oder Short-Covering ohne Käufer-Druck.
- **CVD fällt bei steigendem Preis (Bear-Divergenz)** → klassisches Absorption-Setup: Aggressive Verkäufer treffen passive Käufer-Walls, Preis bewegt sich trotz Aggression nicht in deren Richtung.

## Setups

### Absorption via Delta
Preis macht Higher High, **CVD macht Lower High** (oder bleibt unter vorigem Peak). Lesart: Aggressive Käufer kaufen nicht in derselben Menge wie zuvor, dennoch geht Preis hoch. Eher schwacher Anstieg, Short-Covering. Reversal-Wahrscheinlichkeit erhöht — aber **nicht garantiert**.

### Exhaustion
Vertikale Bewegung mit Delta-Spike, gefolgt von Stagnation. Bsp.: Delta +5.000 in 1 Min, danach 3 Min Preis-Stillstand. Aggressive Käufer haben "ausgeschossen", aber Preis hält nicht; passive Sellers haben absorbiert. Häufiges Top-Signal.

### Bull-Divergenz
Preis macht Lower Low, CVD macht Higher Low. Verkäufer-Aggression nimmt ab, Drawdown wird ausgereizt. Long-Bias.

## Beispiel
BTC-Perpetual auf Binance, 5-Min: Preis steigt von 65k auf 67k, CVD steigt parallel. Bei 67k bildet Preis ein Doppel-Top; im zweiten Top liegt CVD jedoch deutlich unter dem ersten. Eintritt Short auf Bestätigungs-Bar mit negativer Delta-Bar; Stop über Hoch.

## Fallstricke
- **Feed-Abhängigkeit**: CVD an einer einzelnen Börse (z.B. Binance) ignoriert Coinbase/OKX/Bybit. Cross-Exchange-CVD kann gegenläufig sein. Bei Aktien gilt das wegen US-Fragmentierung verschärft.
- **CVD-Reset**: Wahl des Anchor-Punkts ändert die Aussage komplett. Daily-CVD vs. Session-CVD vs. Weekly-CVD erzählen unterschiedliche Geschichten.
- **Klassifikationsbias**: Lee/Ready ~85% akkurat (Aktien). Bei HFT-dominierten Märkten gibt es viele Midpoint- und Hidden-Trades, die systematisch falsch zugeordnet werden (Easley et al. argumentieren u.a. deshalb für **Bulk Volume Classification** über VPIN).
- **Spotting-Bias**: Divergenzen sind retrospektiv leicht zu finden. Eine echte Divergenz-Statistik (Hit-Rate, Reward/Risk) ist in der Edutainment-Literatur fast nie zu sehen.
- **CVD ≠ Open Interest**: CVD trackt Aggressor-Flow, sagt nichts über Position-Building (dafür OI).

## Quellen
- [Bookmap — How Cumulative Volume Delta Can Transform Your Trading Strategy](https://bookmap.com/blog/how-cumulative-volume-delta-transform-your-trading-strategy)
- [ATAS — CVD Pro. How to Use the Cumulative Volume Delta](https://atas.net/volume-analysis/basics-of-volume-analysis/cvd-pro/)
- Easley, D., López de Prado, M., & O'Hara, M. (2012). "Flow Toxicity and Liquidity in a High-Frequency World." *Review of Financial Studies*, 25(5), 1457-1493. [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1695596)

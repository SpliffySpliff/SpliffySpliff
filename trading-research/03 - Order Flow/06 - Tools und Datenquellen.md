# Tools & Datenquellen für Order Flow

## Plattformen (Stand 2026, ungefähre Preise)

| Plattform | Preis (Software) | Stärken | Schwächen |
|---|---|---|---|
| **Sierra Chart** | ~$36/Mon (Service Package 5–11) | Sehr schnell, tiefe Anpassung, gute MBO-Unterstützung, etabliert für Pro-Scalper. | UI altbacken; steile Lernkurve. |
| **ATAS** | ~$85-98/Mon | Saubere Footprint-Implementierung, viele Order-Flow-Indikatoren, EU-Markt verbreitet. | Pro-Subscription nötig für volle Features; Marketing schwer von Inhalt zu trennen. |
| **Bookmap** | ab ~$250/Mon (Global+ Plan; Lower-Tier günstiger, aber ohne Heatmap-Voll-Features) | Beste 2D-Heatmap-Visualisierung; 40 FPS; Add-ons (Stops & Icebergs, BigTrades). | Teuer; viele Add-ons separat kostenpflichtig; eher Visualisierung als Trading-Frontend. |
| **NinjaTrader 8** | "Lifetime" $1.099 oder Free mit höheren Commissions; Order-Flow-Plus separat | Beliebt in USA, Order Flow Plus Add-on bietet Footprint, Heatmap, Imbalance. | Order-Flow-Module historisch nicht so granular wie ATAS. |
| **Quantower** | $70/Mon all-in oder $1.590 Lifetime | Modernes UI, Multi-Asset (Futures, Krypto, FX), gute Footprint-Engine. | Jüngeres Tool, kleineres Ökosystem. |
| **Jigsaw Daytradr** | $180/Mon | DOM-fokussiert ("Reconstructed Tape"), beliebt bei Scalpern. | Footprint vorhanden, aber nicht der USP; nur Frontend, braucht Broker-Connection. |

> **Achtung Daten zusätzlich**: Plattform-Lizenz ≠ Datenfeed. CME-Exchange-Fees fallen separat an: ca. **$2-15/Mon (non-pro)** je Produkt, **$85+/Mon (pro)**.

## Datenfeeds

### Rithmic (Marktstandard für Futures Pro)
- Direct Market Access, Tick-to-Trade <250 μs.
- Liefert **MBO** (Market by Order) für CME — unverzichtbar für seriöse Iceberg-Detektion und CVD.
- In Prop-Firmen (Topstep, Apex etc.) Standard-Routing.

### CQG
- Globaler, breiter Exchange-Coverage (CME, EUREX, ICE, etc.).
- Liefert primär **MBP** (Market by Price), kein MBO — für reine Order-Flow-Strategien ein Manko.
- Eingebaute Analytics, Pro-Firmen wie Topstep nutzen es teils.

### dxFeed
- Powerfeed hinter Bookmap und Optimus Flow. Ca. **$19/Mon** Endkunden-Tarif (Stand 2026, je nach Bundle).
- **Kein MBO für CME** — für Heatmap-Visualisierung ok, für tiefes Order-Flow-Detail nicht ideal.
- Coverage: Aktien, Optionen, Futures, FX.

### IQFeed (DTN)
- Mittelpreisig, populär bei Sierra-Chart-Nutzern. Solide Aktien-Tick-Daten.

### Databento
- **Profi-/Quant-Markt**, API-first, Tick-genaue historische und Live-Daten. Direkt von CME-Colocation.
- Bietet **GLBX.MDP3 (CME Globex MDP 3.0)** als L3/MBO-Feed.
- Pay-per-GB-Modell, sehr fair für Backtesting und Quant-Forschung.
- Hauptzielgruppe: Entwickler und systematische Trader, **kein Chart-Frontend**.

### Polygon.io
- Aktien- und Krypto-fokussiert, gute REST/Websocket-API.
- Liefert L2 für US-Equities (SIP-Feed + Nasdaq); **keine CME Futures L2** in Standardplänen.
- Stärken: Optionen, historische Tick-Daten Aktien.

### Interactive Brokers (IBKR) Level 2
- Über TWS verfügbar, Exchange-Subscriptions einzeln.
- **Latenz-Snapshots** (typisch 100ms+), nicht in Realtime-Feed-Qualität für Scalper.
- Solide für Tickets-pro-Klick-Trader, ungeeignet als Bookmap-/Sierra-Backend für ernsthafte Order-Flow-Analyse.
- Reuters Recap: IBKR ist Broker, nicht Datenanbieter — die Feeds sind für Discretionary-Trading ok, für Microstructure-Forschung **zu grob**.

## Empfehlung nach Use Case
- **Futures-Daytrader, Order Flow**: Sierra Chart oder ATAS + Rithmic.
- **Visuelle Liquiditätsanalyse**: Bookmap + dxFeed (oder Rithmic gegen Aufpreis).
- **Quant/Backtesting**: Databento (GLBX.MDP3) + eigene Python-Pipeline.
- **Aktien-Order-Flow**: schwierig, weil 16+ Venues fragmentieren. Polygon.io + manuelle Aggregation; institutionell: Nasdaq TotalView oder ARCABook direkt.
- **Krypto**: Tardis.dev (Top-Tier historische L2-Daten) oder Direct-Exchange-Feeds Binance/Coinbase/OKX.

## Fallstricke
- **"Free" Datenfeeds** in TradingView / Brokern sind oft **aggregiert oder verzögert**. Order-Flow-Strategien darauf zu validieren ist unzuverlässig.
- **Pro vs. Non-Pro Status**: CME unterscheidet Privat- (cheap) und Pro-User (teuer). Echte Pro-Fees bei einem Multi-Markt-Setup können >$300/Mon kosten.
- **Backfilling**: Live-Feed ≠ historische Feed-Qualität. Manche Feeds verlieren bei Reconnect Microstructure-Events.

## Quellen
- [QuantVPS — Top Order Flow Trading Software](https://www.quantvps.com/blog/order-flow-trading-software)
- [QuantVPS — dxFeed vs Rithmic](https://www.quantvps.com/blog/dxfeed-vs-rithmic-which-market-data-feed-should-you-choose)
- [Databento — CME Globex MDP 3.0 Dataset Specs](https://databento.com/datasets/GLBX.MDP3)
- [CME Group — Market by Order (MBO)](https://www.cmegroup.com/education/market-by-order-mbo.html)

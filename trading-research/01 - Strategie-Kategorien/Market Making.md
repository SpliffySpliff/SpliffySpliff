---
tags: [strategie/marketmaking, evidenz/stark, kategorie, kritisch]
status: recherche
zeitebene: [scalping, hft]
evidenz: stark
quellen:
  - "Avellaneda, Stoikov (2008)"
  - "Glosten, Milgrom (1985)"
  - "Cartea, Jaimungal, Penalva (2015)"
---

# Market Making

> Den Spread verdienen — Hauptrisiko ist Adverse Selection.

> [!warning] Realismus
> Für Retail in liquiden Märkten (ES, BTC-PERP) **nicht profitabel** ohne erhebliche Latenz-/Rebate-Vorteile. In Long-Tail-Märkten (kleine Crypto-Pairs, Optionen) möglich.

## Grundidee
Gleichzeitig limitierte **Bid-** und **Ask-Quotes** stellen. Verdient den Spread als Kompensation für Liquiditätsbereitstellung. Inventory wird aktiv gemanagt (Skew der Quotes je nach Position). Hauptrisiko: **Adverse Selection** durch informierte Trader ("Toxic Flow").

## Marktbedingungen
- Liquide, hochfrequente Märkte mit stabilen Spreads
- Two-Sided-Flow (kein einseitiger Aggressor-Druck)
- Niedrige Volatilität (stabile Mid-Price-Schätzer)
- Technologische Infrastruktur: **Co-Location, FPGA, Tick-to-Trade < 10µs** für institutionelles HFT

## Schwächen
- **Adverse Selection** durch informierte Flow (vgl. VPIN, [[03 - Order Flow/06 - Tools und Datenquellen]])
- **Inventory-Risk** in Trendphasen — einseitige Fills, kein Gegen-Hedge
- Plötzliche Volatilitäts-Ausbrüche → MM-Withdrawal (Flash Crash 6. Mai 2010)
- Hohe Fixkosten (Infrastruktur, Memberships)
- Regulatorisches Risiko: Tick-Size-Pilots, Maker-Taker-Rebates können verschwinden

## Zeitebenen
Mikrosekunden–Sekunden (HFT). Halb-automatisierte Varianten auf Minuten in weniger liquiden Märkten (Crypto, Optionen).

## Sub-Varianten
- **Avellaneda-Stoikov** — Inventory-Modell, Standard in der Literatur
- **Ho-Stoll (1981)** — klassisches Dealer-Modell
- **Glosten-Milgrom (1985)** — Spread-Modell mit asymmetrischer Information
- **Crypto-MM** — Hummingbot, Wintermute-Style

## Verwandte Notizen
- Adverse Selection messen: [[03 - Order Flow/06 - Tools und Datenquellen]] (VPIN)
- Microstructure: [[03 - Order Flow/05 - Order Book Analyse DOM Bookmap]]

## Quellen
- Avellaneda, Stoikov (2008): *High-frequency trading in a limit order book*, QF 8(3) — [PDF](https://people.orie.cornell.edu/sfs33/LimitOrderBook.pdf)
- Ho, Stoll (1981): *Optimal Dealer Pricing under Transactions and Return Uncertainty*, JFE 9(1)
- Glosten, Milgrom (1985): *Bid, Ask and Transaction Prices in a Specialist Market*, JFE 14
- Cartea, Jaimungal, Penalva (2015): *Algorithmic and High-Frequency Trading*, CUP
- O'Hara, M. (1995): *Market Microstructure Theory*, Blackwell

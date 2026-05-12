---
tags: [strategie/volumeprofile, volumeprofile, evidenz/mittel, kategorie]
status: recherche
zeitebene: [intraday, swing]
evidenz: mittel
quellen:
  - "Steidlmayer, Hawkins (2003)"
  - "Dalton, Jones, Dalton (2007)"
  - "Steidlmayer, Koy (1986)"
---

# Volume-Profile-basierte Ansätze

> Volumenverteilung **über Preisniveaus** (statt Zeit) — wo wurde Wert akzeptiert, wo abgelehnt?

![[Bilder/volume-profile-schema.svg]]

## Grundidee
Identifiziert **Akzeptanz- vs. Ablehnungszonen**:
- **POC** (Point of Control) — Preis mit höchstem Volumen
- **Value Area** — Bereich mit typisch 70 % des Volumens
- **High Volume Nodes (HVN)** — Konsolidierungs-Magnete
- **Low Volume Nodes (LVN)** — schnelle Durchquerungszonen, oft Reversal-Punkte

Annahme: Preis kehrt zur **fairen Wert-Zone** (POC) zurück — *oder* bricht klar durch und etabliert eine neue Zone.

## Marktbedingungen
Entstanden für Futures-Pit-Märkte (CBOT 1980er, Steidlmayer). Funktioniert gut in:
- Liquiden Futures (ES, ZB, CL, Gold) mit konzentriertem Volumen
- Klar definierten Sessions mit Open/Close
- Range- und Konsolidierungsphasen

Auction-Market-Theory liefert konzeptionellen Rahmen.

## Schwächen
- **Wenig peer-reviewed Evidenz** — überwiegend Praktiker-Literatur
- Volume Profile aus aggregiertem Tape ist in **fragmentierten Märkten** unvollständig (US Cash Equities über mehrere Venues, Crypto über mehrere Exchanges)
- Signale sind oft diskretionär — schwer zu backtesten
- Konzepte überlappen mit klassischen Support/Resistance ohne klaren Edge-Beweis
- Composite Profile über lange Zeiträume "schmiert" und wird unbrauchbar

## Zeitebenen
- Intraday: Daily Profile
- Swing: Weekly Profile, Composite über Wochen/Monate

## Sub-Varianten
- **Market Profile / TPO** (Steidlmayer original — zeitbasiert) → [[04 - Volume Profile/04 - Market Profile TPO]]
- **Volume Profile** (modern — volumenbasiert) → [[04 - Volume Profile/01 - Volume Profile Grundlagen]]
- **Composite Profile** — Aggregation über mehrere Tage/Wochen
- **VWAP** als verwandtes Konzept → [[04 - Volume Profile/03 - VWAP und Anchored VWAP]]

## Verwandte Notizen
- [[04 - Volume Profile/01 - Volume Profile Grundlagen]]
- [[04 - Volume Profile/02 - POC Value Area VAH VAL]]
- [[04 - Volume Profile/04 - Market Profile TPO]]
- [[04 - Volume Profile/03 - VWAP und Anchored VWAP]]
- [[04 - Volume Profile/05 - Kombinierte Anwendung]]
- Synthesevorschlag: [[05 - Strategievorschläge/Vorschlag B - Mean Reversion am Value Area Edge]]

## Quellen
- Steidlmayer, Hawkins (2003): *Steidlmayer on Markets: Trading with Market Profile*, 2nd ed., Wiley
- Steidlmayer, Koy (1986): *Markets and Market Logic*, Porcupine Press
- Dalton, Jones, Dalton (2007): *Mind Over Markets*, Wiley
- CME Group: *CBOT Market Profile Handbook* (historisches Originaldokument)

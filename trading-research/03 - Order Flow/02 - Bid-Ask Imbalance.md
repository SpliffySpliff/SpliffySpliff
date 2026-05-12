# Bid/Ask Imbalance

## Definition
**Bid/Ask Imbalance** misst die prozentuale Übergewichtung einer Seite des Order Flow auf einem einzelnen Preis-Level innerhalb eines Footprint-Bars. Üblich ist die **diagonale Variante** (ATAS, Sierra Chart, Quantower):

> Ask-Volume auf Preis P wird verglichen mit Bid-Volume auf Preis P − 1 Tick (und umgekehrt).

Die Logik: Wer aggressiv am Ask kauft, sieht das *nächsthöhere* Bid; ein Vergleich auf dem gleichen Preis-Slot wäre verzerrt, weil dort beide Seiten dieselbe Order-Queue gegenüberstehen.

## Typische Schwellenwerte
- **ATAS-Default: 150%** (also Ask ≥ 1,5 × Bid des darunterliegenden Levels).
- **Profi-Setting: 300%** (Ask ≥ 3 × Bid). Bei 300-400% spricht ATAS-Doku selbst von "substantial imbalance".
- Bookmap und Sierra Chart erlauben ähnliche Settings.

Diese Schwellen sind **konventionell, nicht empirisch hergeleitet**. Es gibt keine akademische Studie, die 300% als optimalen Cutoff validiert — der Wert hat sich in der Community etabliert.

## Nutzung als Signal
1. **Einzelne Imbalance**: Schwach. Allein zu unspezifisch.
2. **Stacked Imbalances** (3+ konsekutive Preisebenen auf derselben Seite): markieren oft Support/Resistance-Zonen. Diese Zonen werden statistisch oft erneut getestet.
3. **Imbalance an Schlüssel-Levels** (VAH/VAL, vorheriger HOD/LOD): Bestätigung von Reaktion oder Breakout-Stärke.
4. **Imbalance + Delta-Divergenz**: starkes Buy-Imbalance, aber Preis fällt → Absorption-Hinweis.

## Beispiel
NQ-Future 1-Min-Footprint: An vorheriger Sessions-VAL (16.450) erscheinen 4 gestackte Buy-Imbalances bei 400%. Der Tief-Kerze schließt im oberen Drittel der Bar. Lesart: Aggressive Shorts wurden von passiven Limit-Käufern absorbiert. **Long-Setup** mit Stop wenige Ticks unter dem Tief, Ziel POC der Vorsession.

## Limitations / Fallstricke
- **Klassifikationsfehler 15-25%**: Die Bid/Ask-Zuordnung jeder Trade basiert auf Tick-Rule/Lee-Ready-Heuristiken. Bei volatilen, schnellen Märkten oder Midpoint-Trades fehlerhaft (Odders-White 2000).
- **Iceberg-Verzerrung**: Wenn ein passiver Limit-Buyer Eis am Bid hat (1.000 Lot iceberg, aber sichtbar nur 50), wirken aggressive Verkäufe wie "free" Sell-Volume — das Imbalance-Verhältnis täuscht.
- **Spoofing**: Vorab gepostete, dann gepullte Orders können scheinbare Imbalance erzeugen ohne reale Aggression (gilt v.a. für DOM, nicht für getradete Volumen — daher Footprint-Imbalance ist weniger spoofing-anfällig als DOM-Analyse).
- **Niedrige Volumen-Slots**: 5 vs. 1 Lot ergibt 500% — statistisch bedeutungslos. Mindest-Volumen-Filter setzen (z.B. ≥ 10-20 Lots ES, ≥ 5 NQ).
- **Marketing-Übertreibung**: ATAS- und Bookmap-Blogs präsentieren Imbalance gerne als "edge". Tatsächlich ist es nur ein **kontextabhängiger Hinweis**, kein eigenständiges Signal.

## Quellen
- [ATAS — Imbalance: what is it? How to find and trade imbalance](https://atas.net/atas-possibilities/cluster-charts-footprint/how-to-find-and-trade-imbalance/)
- [ATAS — Imbalance: trade on the side of superior forces](https://atas.net/volume-analysis/basics-of-volume-analysis/imbalance-trade-on-the-side-of-superior-forces/)
- Odders-White, E. R. (2000). "On the occurrence and consequences of inaccurate trade classification." *Journal of Financial Markets*, 3(3), 259-286.

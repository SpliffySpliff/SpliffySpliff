# CLAUDE.md

Kontext für jede Claude-Code-Web-Session in diesem Repo.

## Was hier läuft

Dieses Repo ist ein **persönlicher Wissens-Vault für Online-Marketing & Ads-Lernen** (Ordner `ads-vault/`). Der Nutzer (Martin, lernend, Region Biel/Seeland CH) baut sich Schritt-für-Schritt Wissen + nutzbare Akquise-Templates auf.

**Hauptsprache: Deutsch (Schweizer Hochdeutsch).** Notizen, Commits, Antworten immer auf Deutsch.

## Aktive Kampagne (Mai 2026): Envy Affiliate

- Vermittler-Provision (10 %) für Webagentur [envy.ch](https://envy.ch)
- Zielgruppe: KMU in der Region Biel/Seeland
- Vollständige Strategie + alle Skripte liegen unter:
  - `ads-vault/06 - Kampagnen-Logbuch/2026-05 - Envy Affiliate - Setup.md` (Herzstück, mit 6 offenen TODOs)
  - `ads-vault/01 - Zielgruppen/Persona - KMU Biel-Seeland.md`
  - `ads-vault/03 - Creatives & Copy/Email-Vorlage - Webdesign Erstkontakt CH.md`
  - `ads-vault/02 - Plattformen/LinkedIn - Social Selling Webdesign-Affiliate.md`
  - `ads-vault/04 - Funnels & Conversion/Affiliate-Funnel Envy.md`
  - `ads-vault/05 - Tracking & Analytics/Rechtliches - Cold-Outreach Schweiz.md`
  - `ads-vault/06 - Kampagnen-Logbuch/Lead-Pipeline Envy.md`
- Vault-Startseite: `ads-vault/00 - Übersicht.md`

## Was als Nächstes ansteht

1. **envy.ch scrapen** — sobald Network-Policy es erlaubt (siehe unten). Daraus Persona + Mail-Skripte Envy-spezifisch verfeinern.
2. **6 TODOs mit Envy-Bekanntem klären** (siehe Setup-Notiz)
3. Erste 10 Lead-Recherchen in der Region Biel/Seeland

## Network-Policy & Firecrawl

Der Nutzer hat die Cloud-Umgebung **„Mainy"** auf **Benutzerdefiniert** umgestellt mit Allowlist u.a. für `envy.ch` und `*.ch`. → `curl` aus dieser Sandbox sollte CH-Sites direkt erreichen.

Eine `firecrawl`-MCP-Konfig liegt in `.claude/settings.json`, aber **wird nur aktiv, wenn der Nutzer `FIRECRAWL_API_KEY` als Env-Variable hinterlegt hat** (free tier bei firecrawl.dev). Solange nicht: `curl` nutzen.

## Präferenzen des Nutzers (wichtig)

- **Minimalistisch antworten** — kurz, klar, ein Schritt nach dem anderen
- **Keine kostenpflichtigen Tools** ohne ausdrückliche Zustimmung (z.B. Cloud-MCP-Server) — Free Tier ist ok, Kreditkarten-Pflicht ist Tabu
- **Browser-only Arbeitsstil** — keine Tools voraussetzen, die lokale Installation brauchen
- **Ehrliche Aufklärung** über Tradeoffs (z.B. Network-Policy, Rechtliches Cold-Outreach)
- Bevorzugt **Markdown-Links mit relativen Pfaden** (klickbar auf GitHub), nicht `[[wiki-links]]`

## Hintergrund Nutzer

- Lernend, Erfahrung mit Dropshipping (versteht E-Com, Ads, Funnels grob)
- Kein etabliertes B2B-Netzwerk, kein LinkedIn (Aufbau geplant)
- Region: Biel/Seeland, zweisprachig DE/FR
- Sorge: niemanden „auf die Nerven gehen", Envys Ruf nicht beschädigen

## Workflow-Konventionen

- **Branch-Strategie**: jede grössere Änderung auf eigenem Branch `claude/<thema>`, PR erstellen, mergen
- **Commit-Stil**: deutsch, knapper Imperativ, kurze Begründung im Body
- **Niemals** Secrets / API-Keys ins Repo committen — nur als Env-Variable

---
marp: true
theme: default
paginate: true
footer: 'IT4Science Days 2026 · Agentic AI Workshop'
style: |
  section {
    background-color: #1a1a1a;
    color: #e8e8e8;
    font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
  }
  h1, h2, h3 {
    color: #ffffff;
    font-weight: 700;
  }
  table {
    margin: 0 auto;
    font-size: 22px;
    border-collapse: collapse;
  }
  table th, table td {
    background-color: #2a2a2a;
    padding: 8px 12px;
    border: 1px solid #555;
    color: #e8e8e8;
  }
  table thead th {
    background-color: #383838;
    color: #ffffff;
    border-bottom: 2px solid #666;
  }
  table tbody tr:nth-child(even) td {
    background-color: #252525;
  }
  p:has(img) {
    margin: 0;
    line-height: 0;
  }
  img {
    border-radius: 8px;
    max-height: 420px;
    max-width: 1123px;
    object-fit: contain;
    display: block;
    margin: 0 auto;
  }
  .columns {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
  }
  /* Speaker badges */
  .speaker {
    position: absolute;
    top: 32px;
    right: 40px;
    padding: 6px 16px;
    border-radius: 20px;
    font-size: 18px;
    font-weight: 600;
    letter-spacing: 0.3px;
    z-index: 10;
  }
  .speaker-christian { background: #14432a; color: #7ee2a8; border: 1px solid #2f9e5f; }
  .speaker-tobias    { background: #1a2f52; color: #8ab8ff; border: 1px solid #3b6fc4; }
  .speaker-both      { background: #4a3a12; color: #ffd88a; border: 1px solid #b88a2e; }
  /* Placeholder boxes for content to be added */
  .todo {
    background: #3a2a10;
    border: 1px dashed #c8902e;
    color: #ffd88a;
    border-radius: 8px;
    padding: 10px 16px;
    font-size: 20px;
    margin-top: 8px;
  }
  .todo strong { color: #ffe9b0; }
  blockquote {
    background: #242424;
    border-left: 4px solid #666;
    border-radius: 0 8px 8px 0;
    padding: 10px 16px;
    font-style: italic;
    color: #d0d0d0;
  }
---

<!-- _class: lead -->

# Agentic AI in der Praxis

## Vom Spec zum produktiven Workflow — ein Workshop mit Hands-on

**IT4Science Days 2026 · Agentic AI Workshop**

Christian Uhl · Tobias Weiß

<!-- notes:
Begrüßung (~1 min). Kurz vorstellen: Wer wir sind, worum es geht.
Ziel: Teilnehmende verlassen den Raum mit eigenem Research-Repo + implementiertem Mini-Change.
-->

---

<!-- _class: lead -->

# Agenda

| Zeit | Thema | Wer |
|------|-------|-----|
| 09:10 | SpecDrivenDevelopment | Christian Uhl |
| 09:40 | Open-Source Toolbox | Tobias Weiß |
| 10:10 | **Hands-on** (Coding + Lit-Review) | beide |
| 10:55 | ☕ Pause | — |
| 11:10 | OpenSource vs. Kommerziell | Christian Uhl |
| 11:40 | Foundation Models | Christian Uhl |
| 12:05 | Harness, Caching & Workflows | beide |
| 12:20 | Use Case: OpenDesk Edu | Tobias Weiß |
| 12:50 | Q&A & Abschluss | beide |

<!-- notes:
Agenda auf 1–2 min durchgehen. Auf das Hands-on und den Use Case als Highlights hinweisen.
Christian übernimmt Block 1, 3, 4 — Tobias Block 2, 6 — Hands-on/Harness/Q&A gemeinsam.
-->

---

<div class="speaker speaker-christian">👤 Christian Uhl</div>

## SpecDrivenDevelopment — Anforderungen als Treiber

Der Engpass ist nicht das Programmieren, sondern die **Anforderungsklärung**.

| Ebene | Rolle |
|-------|-------|
| `specs/` | Source of Truth — Verhalten als Verträge (SHALL/MUST/SHOULD, Given/When/Then) |
| `changes/` | Delta-Specs — `proposal.md` · `specs.md` · `tasks.md` |
| `archive/` | Decision Log — „Warum" bleibt in 6 Monaten beantwortbar |

> Specs sind der Vertrag zwischen Mensch und Agent.

<!-- notes:
CHRISTIAN — Block 1 · 09:10–09:40 (30 min)
→ Intro: Warum Anforderungen der Engpass sind.
→ Grundprinzip specs/changes/archive erklären.
→ Vorteile: klarer Scope, überprüfbare Acceptance Criteria.
→ Übergang: "Specs sind der Treibstoff — die Werkzeuge zeigen wir gleich."
-->

---

<div class="speaker speaker-christian">👤 Christian Uhl</div>

## Delta-Specs: Klarer Scope, überprüfbarer Fortschritt

```yaml
# changes/<name>/specs.md
## ADDED
- helmfile/apps/typo3/values.yaml.gotmpl — OIDC-Client-Konfiguration
## MODIFIED
- openspec/specs/services/typo3/spec.md — Auth: OIDC → OIDC (Keycloak)
## REMOVED
- (none)
```

- Agent bekommt die **exakte Differenz** — keine Klärungsrunden nötig.
- Acceptance Criteria sind an die behaviorale Spec gekoppelt.
- `STATE.md` pro Phase ersetzt das Neuerklären in jeder Agent-Session.

<!-- notes:
CHRISTIAN — vertiefen: Ein Change-Beispiel aus eurer Praxis durchgehen.
→ Mini-Live: bestehende Spec an einem echten Beispiel zeigen.
-->

---

<div class="speaker speaker-christian">👤 Christian Uhl</div>

## SpecDrivenDevelopment — Erfahrungen aus der Praxis

<div class="todo">
  <strong>Platzhalter Christian:</strong> Hier deine eigenen Beispiele, Erfahrungen und
  Lessons Learned aus Spec-driven-Projekten einfügen (z. B. Uni Gießen / ZAID).
  <br/>Vorschläge: Wann lohnt sich OpenSpec? Wann ist es Overhead?
  Welche Fallstricke gibt es bei Delta-Specs im Team?
</div>

<!-- notes:
CHRISTIAN — eigene Praxisbeispiele (5–8 min). Bitte vorab ausfüllen.
-->

---

<!-- _class: lead -->

<div class="speaker speaker-tobias">👤 Tobias Weiß</div>

# Open-Source Toolbox

<!-- notes:
TOBIAS — Sektions-Trenner, Übergang.
-->

---

<div class="speaker speaker-tobias">👤 Tobias Weiß</div>

## OpenCode: Der agentische Coding-Terminal

- **CLI-Agent**, der Code liest, schreibt und testet.
- **Multi-Model-Routing** über LiteLLM (eine Config, beliebige Modelle).
- **30+ parallele Hintergrund-Agenten** mit Context-Kompaktion.
- **LSP + AST-grep**: echtes Code-Verständnis, 25 Sprachen.
- **Plugin-System**: Skills, MCP-Server, Custom-Tools.

<!-- notes:
TOBIAS — Block 2 · 09:40–10:10 (30 min)
→ Kurz: Was ist OpenCode, warum CLI-first.
→ Live/Videos: einen Change durch OpenCode implementieren lassen.
-->

---

<div class="speaker speaker-tobias">👤 Tobias Weiß</div>

## OpenSpec & SAIA Accelerator

| Tool | Funktion |
|------|----------|
| **OpenSpec** | Spec-driven Development Framework — Delta-Specs als Agenten-Prompts |
| **SAIA Accelerator** | Plugin für OpenCode — automatisierte Abläufe, beschleunigte Iteration |
| **Lean** | Kleine Iterationen, schnelles Feedback — Specs als MVP-Backlog |

> Kurzdemo: Ein Change wird per OpenCode + SAIA implementiert.

<!-- notes:
TOBIAS — Kurzdemo oder Video (5 min).
→ Übergang: "Jetzt seid ihr dran!" → Hands-on.
-->

---

<!-- _class: lead -->

<div class="speaker speaker-both">👥 beide</div>

# Hands-on: Jetzt selber machen

<!-- notes:
BEIDE — Sektions-Trenner. Setup-Fragen klären (GitHub-Account, Sandbox).
-->

---

<div class="speaker speaker-both">👥 beide</div>

## Übung 1 — Agentic Coding (OpenSpec-Change)

- Mini-Aufgabe als **OpenSpec-Change** strukturieren (`proposal`/`specs`/`tasks`).
- Implementieren lassen mit **OpenCode/CLI** — kleine, abgegrenzte Aufgabe in einem Übungs-Repo.
- 2–3 kurze Ergebnis-Demos.

<!-- notes:
BEIDE — Übung 1 · ~20 min.
→ Support durch beide Referenten im Raum.
→ Ergebnis-Sampling: 2–3 kurze Demos.
-->

---

<div class="speaker speaker-both">👥 beide</div>

## Übung 2 — Agentic Literature Review

- Start mit dem **skeleton-research**-Repo: eigene Literatur-Review-Corpus aufsetzen.
- `config/taxonomy.yaml` anpassen → `papers.yaml` seeden → Pipeline → CI + Pages.
- Der Agent übernimmt: Discovery, Taxonomie-Zuordnung, Validierung, ersten Bericht.

```bash
git clone https://github.com/tobias-weiss-ai-xr/skeleton-research.git
# → eigenes Thema einstellen, Agent laufen lassen, fertig 🚀
```

> Ergebnis: **jeder verlässt den Raum mit einem eigenen, CI-validierten Research-Repo.**

<!-- notes:
BEIDE — Übung 2 · ~20 min.
→ skeleton-research-Repo: github.com/tobias-weiss-ai-xr/skeleton-research
→ Kurze Live-Demo: config/taxonomy.yaml anpassen + ersten Lauf zeigen.
-->

---

<!-- _class: lead -->

<div class="speaker speaker-christian">👤 Christian Uhl</div>

# OpenSource vs. Kommerziell

<!-- notes:
CHRISTIAN — Sektions-Trenner Block 3.
-->

---

<div class="speaker speaker-christian">👤 Christian Uhl</div>

## OpenCode vs. Claude Code vs. Alternativen

| Aspekt | OpenCode (OS) | Claude Code (kommerziell) |
|--------|---------------|---------------------------|
| Preis | Kostenlos, eigene Infra | Abo-/API-basiert |
| Datenschutz | Vollständige Kontrolle | Daten beim Anbieter |
| Souveränität | Lokal / eigene GPUs | Cloud-abhängig |
| Steuerbarkeit | Volle Konfig-Freiheit | Vendor-Defaults |
| Lock-in | Kein | Wechselkosten |

> Kein „entweder/oder" — **Mischstrategien** sind die Realität an Hochschulen.

<!-- notes:
CHRISTIAN — Block 3 · 11:10–11:40 (30 min)
→ Vergleich führen, Mischstrategien diskutieren.
→ Interaktion: kurze Abstimmung unter den Teilnehmenden.
-->

---

<div class="speaker speaker-christian">👤 Christian Uhl</div>

## OpenSource vs. Kommerziell — Praxis-Einordnung

<div class="todo">
  <strong>Platzhalter Christian:</strong> Deine Perspektive einfügen —
  z. B. Erfahrungen aus Uni-Gießen-Projekten, Entscheidungskriterien für
  Hochschulen (Budget, DSGVO, eigene Infra), aktuelle Zahlen/Tendenzen.
</div>

<!-- notes:
CHRISTIAN — eigene Praxisbeispiele + Takeaway für Hochschulen.
-->

---

<!-- _class: lead -->

<div class="speaker speaker-christian">👤 Christian Uhl</div>

# Foundation Models — aktuelle Entwicklungen

<!-- notes:
CHRISTIAN — Sektions-Trenner Block 4.
-->

---

<div class="speaker speaker-christian">👤 Christian Uhl</div>

## Was 2026 relevant ist

- **OpenSource vs. proprietär**: Capabilities, Kontextlänge, Agentic-Fähigkeiten, Kosten.
- **Neuerungen**: Funktionen-Calls, **MCP**, Reasoning-Modelle, lokale Modelle (Ollama).
- **Tool-Using & Multi-Agent** werden Standard.
- Lokale Modelle: Souveränität + Datenschutz ohne Qualitätsverlust bei vielen Tasks.

<!-- notes:
CHRISTIAN — Block 4 · 11:40–12:05 (25 min)
→ Überblick + Ausblick & Trends.
-->

---

<div class="speaker speaker-christian">👤 Christian Uhl</div>

## Foundation Models — eure Fragen & Fokus

<div class="todo">
  <strong>Platzhalter Christian:</strong> Hier aktuelle Modell-Landschaft einfügen
  (OpenSource vs. proprietär), Kontextlänge/Agentic-Fähigkeiten, und euren
  Ausblick 2026/2027. Gerne mit euren Lieblingsbeispielen und Live-Demos.
</div>

<!-- notes:
CHRISTIAN — eigene Inhalte (10–15 min). Bitte vorab ausfüllen.
-->

---

<!-- _class: lead -->

<div class="speaker speaker-both">👥 beide</div>

# Agent-Harness, Caching & Workflows

<!-- notes:
BEIDE — Sektions-Trenner Block 5.
-->

---

<div class="speaker speaker-both">👥 beide</div>

## Der Harness ist die Steuerungsebene

| Baustein | Funktion |
|----------|----------|
| Kontext-/Memory-Management | Was sieht der Agent? |
| Tool-Registry | Welche Werkzeuge sind erlaubt? |
| Skills | Wiederverwendbare Workflow-Vorlagen |
| Prompt-Templates | Stabile Anweisungen |
| Evaluation/Sandboxing | Sicher testen |

> Gleiche Modelle, unterschiedliche Ergebnisse — **je nach Harness**.

<!-- notes:
BEIDE — Block 5 · 12:05–12:20 (15 min)
→ Harness als Steuerungsebene: pi, OpenCode, Oh-My-OpenAgent.
-->

---

<div class="speaker speaker-both">👥 beide</div>

## Caching: Effizienz & Kosten

- **Prompt-/KV-Caching**: Kontext-Wiederverwendung über Steps.
- **Schema-/Spec-Caching**: wiederkehrende Strukturen nicht neu berechnen.
- Senkt Latenz und Tokenkosten bei langen Agent-Sessions.

---

<div class="speaker speaker-both">👥 beide</div>

## Workflows als „Muskelgedächtnis"

> **Das Modell ist das Gehirn, die Workflows sind der Muskel.**

- Wiederkehrende Abläufe (Spec → Change → Deploy → Verify → Report) als **wiederverwendbare Routinen** verankern.
- Qualität wird reproduzierbar, Wissen wandert in den Workflow statt in jede Session neu erklärt zu werden.

<!-- notes:
BEIDE — Übergang zum Use Case: "Dieses Steuerungs- & Workflow-Wissen setzen wir jetzt in einem realen System um → OpenDesk Edu."
-->

---

<!-- _class: lead -->

<div class="speaker speaker-tobias">👤 Tobias Weiß</div>

# Use Case: OpenDesk Edu

<!-- notes:
TOBIAS — Sektions-Trenner Block 6.
-->

---

<div class="speaker speaker-tobias">👤 Tobias Weiß</div>

## openDesk Edu — die Plattform

- **openDesk CE** (BSI-zertifiziert, souverän) **+ 25 Bildungs- & Forschungsdienste**.
- Lernplattformen (ILIAS, Moodle) · Sci-Computing (JupyterHub, Overleaf, RStudio, Dask) · lokale KI (Open WebUI + Ollama) · Lehre-Video (BigBlueButton).
- **Ein Deployment** (`helmfile apply`), **ein Login** (Keycloak), **ein Backup-System** (k8up).

<!-- notes:
TOBIAS — Block 6 · 12:20–12:50 (30 min) · Detailplan: docs/plan-opendesk-edu-teil.md
→ Plattform in 5 min (Demo: Portal, Landscape).
-->

---

<div class="speaker speaker-tobias">👤 Tobias Weiß</div>

## Agentic Engineering Showcase

```
Idee → OpenSpec Change (proposal/specs/tasks) → Agent (OpenCode + SAIA)
     → Tests (pytest, Playwright) → Merge → helmfile apply → Betrieb
```

- **ILIAS-Integration**: SAML NameFormat, Shibboleth SP, `shib_activate_new=0`, Timeout 60→300 s, stündlicher HealthCheck.
- **Skalierung**: 25 Charts, SSO-Audit 44/44 Clients, 33/33 Services mit SSO.
- **Ralph-Loop**: Betriebserkenntnisse → neue Specs → neue Changes.
- **opendesk-dev-agent**: Knowledge Graph + Experience-Memory per Slash-Command.

<!-- notes:
TOBIAS — Kern des Blocks: Showcase vom Change-Proposal zum deployed Service.
→ Live am Beispiel ILIAS-Integration (echte Lessons Learned).
-->

---

<div class="speaker speaker-tobias">👤 Tobias Weiß</div>

## Zahlen, die beeindrucken

| Metrik | Wert |
|--------|------|
| Dienste | 25+ (LMS, Sci-Computing, KI, Kollaboration) |
| Pods | 97/97 laufen |
| SSO-Services | 33/33 |
| Keycloak-Clients | 44/44 auditiert |
| Specs | 56 (24 Services, 17 Platform, 4 Auth, 6 Integrations, 5 Registry) |
| Backups | 5 CronJobs aktiv, 14 d Retention |

<!-- notes:
TOBIAS — Live-Demo Betrieb: SSO-E2E, kubectl, Grafana, Backups.
-->

---

<div class="speaker speaker-tobias">👤 Tobias Weiß</div>

## Ehrliche Hürden

- **Institutionell > technisch**: Rechtsabteilung (DSGVO, AVV), Personalrat, Verwaltung.
- **Agenten-Halluzinationen**: nur durch Tests, HealthChecks und Review abzufangen.
- **Upstream-Drift**: eigene Images & Security-Patching stehen auf der Roadmap.
- **Ops-Wissen bleibt nötig**: K8s, Keycloak, Helm — Agenten beschleunigen, Menschen verantworten.

<!-- notes:
TOBIAS — Ehrlichkeit schafft Glaubwürdigkeit. Kurz halten.
-->

---

<!-- _class: lead -->

<div class="speaker speaker-both">👥 beide</div>

# Wrap Up

<!-- notes:
BEIDE — Abschluss.
-->

---

<div class="speaker speaker-both">👥 beide</div>

## Das Muster auf eigene Projekte übertragen

1. **Klein starten**: eine Spec für ein vorhandenes Modul (Given/When/Then).
2. **Delta-Specs nutzen**: erster Change mit 3 Tasks → Agent implementieren lassen.
3. **Verifikation erzwingen**: Tests + Review als Pflicht — Agenten iterieren lassen.
4. **Wissen persistieren**: pi-memory/Knowledge Graph ab Session 1.
5. **Loop institutionalisieren**: Betriebserkenntnisse werden Changes.

<!-- notes:
BEIDE — Takeaway-Material zeigen (Links).
-->

---

<div class="speaker speaker-both">👥 beide</div>

## Resources

- **OpenCode** — github.com/sst/opencode
- **OpenSpec** — github.com/FissionAI/OpenSpec
- **SAIA Accelerator** — codeberg.org/graphwiz-ai/opencode-saia-plugin
- **openDesk Edu** — github.com/opendesk-edu/opendesk-edu · opendesk-edu.org
- **skeleton-research** — github.com/tobias-weiss-ai-xr/skeleton-research
- **Superpowers Skills** — github.com/obra/superpowers

<!-- notes:
Links können als QR-Code oder Handout ergänzt werden.
-->

---

<!-- _class: lead -->

<div class="speaker speaker-both">👥 beide</div>

# Questions & Discussion

Vielen Dank!

Diskussionsthemen:
- Wo liegt das größte Potenzial — und wo die größte Skepsis?
- Governance-Regeln für agentische Systeme?
- Eigene Modelle auf lokaler Hardware?
- Agentische Literatur-Reviews für Ihre Forschung?

<!-- notes:
BEIDE — Moderation: Erfahrungsaustausch & Anwendungsfälle aus Teilnehmenden-Perspektive.
-->

---

# License

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

Christian Uhl · Tobias Weiß — except where otherwise noted.

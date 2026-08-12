---
marp: true
theme: default
paginate: true
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
    font-size: 24px;
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
---

<!-- _class: lead -->

# Agentic AI in der Praxis

## Vom Spec zum produktiven Workflow — ein Workshop mit Hands-on

IT4Science Days 2026 · Agentic AI Workshop

Christian Uhl · Tobias Weiß

---

<!-- _class: lead -->

# Agenda

- SpecDrivenDevelopment — Anforderungen als Treiber
- Open-Source Toolbox — OpenCode, OpenSpec, Lean & SAIA
- Hands-on: Agentic Coding + Agentic Literature Review
- OpenSource vs. Kommerziell
- Aktuelle Entwicklungen bei den Foundation Models
- Agent-Harness, Caching & Workflows
- Use Case: OpenDesk Edu
- Wrap Up

---

## SpecDrivenDevelopment — Anforderungen als Treiber

Der Engpass ist nicht das Programmieren, sondern die **Anforderungsklärung**.

| Ebene | Rolle |
|-------|-------|
| `specs/` | Source of Truth — Verhalten als Verträge (SHALL/MUST/SHOULD, Given/When/Then) |
| `changes/` | Delta-Specs — `proposal.md` · `specs.md` · `tasks.md` |
| `archive/` | Decision Log — „Warum" bleibt in 6 Monaten beantwortbar |

> Specs sind der Vertrag zwischen Mensch und Agent.

---

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

---

<!-- _class: lead -->

# Open-Source Toolbox

---

## OpenCode: Der agentische Coding-Terminal

- **CLI-Agent**, der Code liest, schreibt und testet.
- **Multi-Model-Routing** über LiteLLM (eine Config, beliebige Modelle).
- **30+ parallele Hintergrund-Agenten** mit Context-Kompaktion.
- **LSP + AST-grep**: echtes Code-Verständnis, 25 Sprachen.
- **Plugin-System**: Skills, MCP-Server, Custom-Tools.

---

## OpenSpec & SAIA Accelerator

| Tool | Funktion |
|------|----------|
| **OpenSpec** | Spec-driven Development Framework — Delta-Specs als Agenten-Prompts |
| **SAIA Accelerator** | Plugin für OpenCode — automatisierte Abläufe, beschleunigte Iteration |
| **Lean** | Kleine Iterationen, schnelles Feedback — Specs als MVP-Backlog |

> Kurzdemo: Ein Change wird per OpenCode + SAIA implementiert.

---

<!-- _class: lead -->

# Hands-on: Jetzt selber machen

---

## Übung 1 — Agentic Coding (OpenSpec-Change)

- Mini-Aufgabe als **OpenSpec-Change** strukturieren (`proposal`/`specs`/`tasks`).
- Implementieren lassen mit **OpenCode/CLI** — kleine, abgegrenzte Aufgabe in einem Übungs-Repo.
- 2–3 kurze Ergebnis-Demos.

---

## Übung 2 — Agentic Literature Review

- Start mit dem **skeleton-research**-Repo: eigene Literatur-Review-Corpus aufsetzen.
- `config/taxonomy.yaml` anpassen → `papers.yaml` seeden → Pipeline → CI + Pages.
- Der Agent übernimmt: Discovery, Taxonomie-Zuordnung, Validierung, ersten Bericht.

```bash
git clone https://github.com/tobias-weiss-ai-xr/skeleton-research.git
# → eigenes Thema einstellen, Agent laufen lassen, fertig 🚀
```

> Ergebnis: **jeder verlässt den Raum mit einem eigenen, CI-validierten Research-Repo.**

---

<!-- _class: lead -->

# OpenSource vs. Kommerziell

---

## OpenCode vs. Claude Code vs. Alternativen

| Aspekt | OpenCode (OS) | Claude Code (kommerziell) |
|--------|---------------|---------------------------|
| Preis | Kostenlos, eigene Infra | Abo-/API-basiert |
| Datenschutz | Vollständige Kontrolle | Daten beim Anbieter |
| Souveränität | Lokal / eigene GPUs | Cloud-abhängig |
| Steuerbarkeit | Volle Konfig-Freiheit | Vendor-Defaults |
| Lock-in | Kein | Wechselkosten |

> Kein „entweder/oder" — **Mischstrategien** sind die Realität an Hochschulen.

---

<!-- _class: lead -->

# Foundation Models — aktuelle Entwicklungen

---

## Was 2026 relevant ist

- **OpenSource vs. proprietär**: Capabilities, Kontextlänge, Agentic-Fähigkeiten, Kosten.
- **Neuerungen**: Funktionen-Calls, **MCP**, Reasoning-Modelle, lokale Modelle (Ollama).
- **Tool-Using & Multi-Agent** werden Standard.
- Lokale Modelle: Souveränität + Datenschutz ohne Qualitätsverlust bei vielen Tasks.

---

<!-- _class: lead -->

# Agent-Harness, Caching & Workflows

---

## Der Harness ist die Steuerungsebene

| Baustein | Funktion |
|----------|----------|
| Kontext-/Memory-Management | Was sieht der Agent? |
| Tool-Registry | Welche Werkzeuge sind erlaubt? |
| Skills | Wiederverwendbare Workflow-Vorlagen |
| Prompt-Templates | Stabile Anweisungen |
| Evaluation/Sandboxing | Sicher testen |

> Gleiche Modelle, unterschiedliche Ergebnisse — **je nach Harness**.

---

## Caching: Effizienz & Kosten

- **Prompt-/KV-Caching**: Kontext-Wiederverwendung über Steps.
- **Schema-/Spec-Caching**: wiederkehrende Strukturen nicht neu berechnen.
- Senkt Latenz und Tokenkosten bei langen Agent-Sessions.

---

## Workflows als „Muskelgedächtnis"

> **Das Modell ist das Gehirn, die Workflows sind der Muskel.**

- Wiederkehrende Abläufe (Spec → Change → Deploy → Verify → Report) als **wiederverwendbare Routinen** verankern.
- Qualität wird reproduzierbar, Wissen wandert in den Workflow statt in jede Session neu erklärt zu werden.

---

<!-- _class: lead -->

# Use Case: OpenDesk Edu

---

## openDesk Edu — die Plattform

- **openDesk CE** (BSI-zertifiziert, souverän) **+ 25 Bildungs- & Forschungsdienste**.
- Lernplattformen (ILIAS, Moodle) · Sci-Computing (JupyterHub, Overleaf, RStudio, Dask) · lokale KI (Open WebUI + Ollama) · Lehre-Video (BigBlueButton).
- **Ein Deployment** (`helmfile apply`), **ein Login** (Keycloak), **ein Backup-System** (k8up).

---

## Agentic Engineering Showcase

```
Idee → OpenSpec Change (proposal/specs/tasks) → Agent (OpenCode + SAIA)
     → Tests (pytest, Playwright) → Merge → helmfile apply → Betrieb
```

- **ILIAS-Integration**: SAML NameFormat, Shibboleth SP, `shib_activate_new=0`, Timeout 60→300 s, stündlicher HealthCheck.
- **Skalierung**: 25 Charts, SSO-Audit 44/44 Clients, 33/33 Services mit SSO.
- **Ralph-Loop**: Betriebserkenntnisse → neue Specs → neue Changes.
- **opendesk-dev-agent**: Knowledge Graph + Experience-Memory per Slash-Command.

---

## Zahlen, die beeindrucken

| Metrik | Wert |
|--------|------|
| Dienste | 25+ (LMS, Sci-Computing, KI, Kollaboration) |
| Pods | 97/97 laufen |
| SSO-Services | 33/33 |
| Keycloak-Clients | 44/44 auditiert |
| Specs | 56 (24 Services, 17 Platform, 4 Auth, 6 Integrations, 5 Registry) |
| Backups | 5 CronJobs aktiv, 14 d Retention |

---

## Ehrliche Hürden

- **Institutionell > technisch**: Rechtsabteilung (DSGVO, AVV), Personalrat, Verwaltung.
- **Agenten-Halluzinationen**: nur durch Tests, HealthChecks und Review abzufangen.
- **Upstream-Drift**: eigene Images & Security-Patching stehen auf der Roadmap.
- **Ops-Wissen bleibt nötig**: K8s, Keycloak, Helm — Agenten beschleunigen, Menschen verantworten.

---

<!-- _class: lead -->

# Wrap Up

---

## Das Muster auf eigene Projekte übertragen

1. **Klein starten**: eine Spec für ein vorhandenes Modul (Given/When/Then).
2. **Delta-Specs nutzen**: erster Change mit 3 Tasks → Agent implementieren lassen.
3. **Verifikation erzwingen**: Tests + Review als Pflicht — Agenten iterieren lassen.
4. **Wissen persistieren**: pi-memory/Knowledge Graph ab Session 1.
5. **Loop institutionalisieren**: Betriebserkenntnisse werden Changes.

---

## Resources

- **OpenCode** — github.com/sst/opencode
- **OpenSpec** — github.com/FissionAI/OpenSpec
- **SAIA Accelerator** — codeberg.org/graphwiz-ai/opencode-saia-plugin
- **openDesk Edu** — github.com/opendesk-edu/opendesk-edu · opendesk-edu.org
- **skeleton-research** — github.com/tobias-weiss-ai-xr/skeleton-research
- **Superpowers Skills** — github.com/obra/superpowers

---

<!-- _class: lead -->

# Questions & Discussion

Vielen Dank!

Diskussionsthemen:
- Wo liegt das größte Potenzial — und wo die größte Skepsis?
- Governance-Regeln für agentische Systeme?
- Eigene Modelle auf lokaler Hardware?
- Agentische Literatur-Reviews für Ihre Forschung?

---

# License

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

Christian Uhl · Tobias Weiß — except where otherwise noted.

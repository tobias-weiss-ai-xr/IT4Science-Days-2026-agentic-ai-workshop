# IT4Science Days 2026 — Agentic AI Workshop: Grobe Gesamt-Zeitplanung

> **Format:** ~4 h 15 min Workshop (255 min inkl. Pause, 09:00–13:15) · **Sprache:** Deutsch
> **Agenda:** SpecDrivenDevelopment → Open-Source Toolbox → **Hands-on** → OpenSource vs. Kommerziell → Foundation Models → Harness/Caching/Workflows → Use Case: OpenDesk Edu → Q&A
> **Referenten:** Christian Uhl (Uni Gießen) · Tobias Weiß (UMR)
> **Detailplanung des OpenDesk-Edu-Teils:** [plan-opendesk-edu-teil.md](plan-opendesk-edu-teil.md)

> **Hinweis Format:** Der Hands-on-Block (F) ist **fest eingeplant** — damit steigt das Format von 3h auf 4h. Sollte das Publikum/der Zeitrahmen strikt bei 3h liegen müssen, wird der Blockschnitt nur bei Block 4/5 gekürzt (siehe [Puffer](#puffer--fallback-strategie)); F und Use Case bleiben geschützt.

---

## Übersicht (4 h)

| # | Block | Zeitfenster | Dauer | Verantwortung |
|---|-------|-------------|-------|---------------|
| 0 | Ankommen & Rahmen | 09:00–09:10 | 10 min | beide |
| 1 | SpecDrivenDevelopment — Anforderungen als Treiber | 09:10–09:40 | 30 min | Christian |
| 2 | Open-Source Toolbox (OpenCode, OpenSpec, Lean + SAIA) | 09:40–10:10 | 30 min | Tobias |
| F | **Hands-on: Agentic Coding + Agentic Literature Review** (zwei Übungen) | 10:10–10:55 | 45 min | Tobias/Christian |
| — | *Kaffeepause* | 10:55–11:10 | 15 min | — |
| 3 | OpenSource vs. Kommerziell (OpenCode vs. Claude Code) | 11:10–11:40 | 30 min | Christian |
| 4 | Aktuelle Entwicklungen bei den Foundation Models | 11:40–12:05 | 25 min | Christian |
| 5 | Agent-Harness, Caching & Workflows | 12:05–12:20 | 15 min | Tobias/Christian |
| 6 | **Use Case: OpenDesk Edu** (Agentic Engineering) | 12:20–12:50 | 30 min | Tobias |
| 7 | Q&A / Abschluss-Diskussion | 12:50–13:15 | 25 min | beide |

**Gesamt:** ~240 min Inhalt inkl. Hands-on (Block F) + 15 min Pause = **255 min (4 h 15 min), 09:00–13:15**

**Lernlogik der Reihenfolge:**
Grundlage (SpecDriven) → Werkzeuge (Toolbox) → **sofort anwenden (Hands-on)** → Kontext (Vergleich & Modelle) → Technik (Harness/Caching/Workflows) → Praxis (OpenDesk Edu) → Austausch (Q&A).

---

## Blockweise Grobplanung

### Block 1 — SpecDrivenDevelopment (09:10–09:40, 30 min) · **Christian**
- Intro: Warum Anforderungen der Engpass sind (nicht das Programmieren).
- Grundprinzip: `specs/` (Source of Truth) + `changes/` (Delta-Specs: proposal/specs/tasks) + `archive/` (Decision Log).
- Vorteile: klarer Scope, überprüfbare Acceptance Criteria, Agenten-taugliche Prompts.
- Mini-Live: eine bestehende Spec an einem echten Beispiel (z. B. aus openDesk-Edu-Spec).
- Übergang: "Specs sind der Treibstoff — die Werkzeuge zeigen wir gleich."

### Block 2 — Open-Source Toolbox (09:40–10:10, 30 min) · **Tobias**
- **OpenCode** (agentischer Coding-Terminal, offen).
- **OpenSpec** (Spec-driven Development Framework).
- **Lean / Lean Methodology** im Werkzeug-Kontext (kleine Iterationen, Feedback).
- **SAIA Accelerator** (Plugin für OpenCode): demonstrierte automatisierte Abläufe.
- Kurzdemo oder Video: einen Change durch OpenCode+SAIA implementieren lassen.
- Übergang: spezifikationsbasiert → direkt selbst ausprobieren.

### Block F — Hands-on: Agentic Coding + Agentic Literature Review (10:10–10:55, 45 min) · **Tobias/Christian** ⭐ interaktiv

**Übung 1 — Agentic Coding (20 min)**
- Teilnehmende strukturieren eine Mini-Aufgabe als OpenSpec-Change (`proposal`/`specs`/`tasks`).
- Anschließend implementieren lassen (OpenCode/CLI) — als kleine, abgegrenzte Aufgabe (z. B. Funktions-Erweiterung in einem Übungs-Repo, nicht Produktions-Repo).
- Vorbereitetes Sandbox-Projekt + vorgegebene Tasks; Support-Assistenz beider Referenten.
- Ergebnis-Sampling: 2–3 kurze Demos, worum es ging und was die Agenten geliefert haben.

**Übung 2 — Agentic Literature Review (20 min)**
- Jeder wählt sein eigenes Forschungsthema und startet mit dem **skeleton-research**-Repo: [github.com/tobias-weiss-ai-xr/skeleton-research](https://github.com/tobias-weiss-ai-xr/skeleton-research)
- Schnellstart in 5 Schritten: `config/taxonomy.yaml` anpassen (Thema, Kategorien, Queries) → `papers.yaml` seeden → Pipeline ausführen → CI + GitHub Pages aktivieren.
- Agent übernimmt: ersten Literatur-Discovery-Lauf (`fetch_new_papers.py`), automatische Taxonomie-Zuordnung, Validierung und die Generierung des ersten `literature_review.md`-Berichts.
- Ergebnis: jeder verlässt den Raum mit einem **eigenen, CI-validierten Research-Repo** + erstem Bericht.
- Material: Übungsanleitung + Beispiel-Taxonomien liegen im Repo (README + AGENTS.md).

- Übergang: "Ihr habt selbst entwickelt und euer eigenes Research-Repo gestartet — jetzt die Einordnung: OpenSource vs. kommerziell, und welche Modelle dahinterstecken."
- **Vorlauf:** Setups (Sandbox, GitHub-Account, Keys, Browser) 2 Wochen vorher verteilen; skeleton-research-Repo vorab klonen.

### ☕ Pause — 10:55–11:10 (15 min)

### Block 3 — OpenSource vs. Kommerziell (11:10–11:40, 30 min) · **Christian**
- Vergleich OpenCode vs. Claude Code vs. Alternativen (Preis, Datenschutz, Souveränität, Steuerbarkeit, Vendor-Lock-in).
- Kein "entweder/oder"-Dogma: Mischstrategien.
- Practical Takeaways für Hochschulen (Budget, DSGVO, eigene Infra).
- Interaktion: kurze Abstimmung unter den Teilnehmenden.

### Block 4 — Aktuelle Entwicklungen bei den Foundation Models (11:40–12:05, 25 min) · **Christian**
- Überblick aktuelle Modelle (OpenSource vs. proprietär): Capabilities, Kontextlänge, Agentic-Fähigkeiten, Cost.
- Relevante Neuerungen: Funktionen-Calls, MCP, Reasoning-Modelle, lokale Modelle (Ollama).
- Auswirkung auf agentisches Arbeiten (Tool-Using, Multi-Agent).
- Ausblick & Trends, was 2027 in Sicht ist.

### Block 5 — Agent Harness, Caching & Workflows (12:05–12:20, 15 min) · **Tobias/Christian**
> Ersetzt den ursprünglichen Titel „Agile Methoden im KI-Zeitalter“.

- **Harness = Steuerungs-Ebene über dem Modell:** Kontext-/Memory-Management, Tool-Registry, Skills, Prompt-Templates, Evaluation/Sandboxing, sicherer Zugriff auf Repo & Cluster (u.a. pi als Coding-Agent).
- Warum der Harness oft wichtiger ist als das Modell: gleiche Modelle, unterschiedliche Ergebnisse je nach Steuerung.
- **Caching für Effizienz & Kosten:** Prompt-/KV-Caching, Caching zwischen Agent-Steps, Schema-/Spec-Caching; senkt Latenz und Tokenkosten in langen Sessions.
- **Workflows als „Muskelgedächtnis“:** Das Modell ist das Gehirn, die Workflows der Muskel — wiederkehrende Abläufe (Spec → Change → Deploy → Verify → Report) als wiederverwendbare Fähigkeiten verankern.
- Übergang: „Dieses Steuerungs- & Workflow-Wissen setzen wir jetzt in einem realen System um → OpenDesk Edu.“

### Block 6 — Use Case: OpenDesk Edu (12:20–12:50, 30 min) · **Tobias**
> **Detailplan:** [plan-opendesk-edu-teil.md](plan-opendesk-edu-teil.md)
- Plattform in 5 min (Demo: Portal, Landscape).
- **Agentic Engineering Showcase (Kern):** vom OpenSpec-Change zum deployed Service, ILIAS-Integration, Skalierung auf 25 Dienste, Ralph-Loop & opendesk-dev-agent.
- Live-Demo Betrieb: SSO, kubectl, Grafana, Backups.
- Lessons Learned & ehrliche Hürden.
- Takeaway: übertragbares Muster.

### Block 7 — Q&A / Abschluss-Diskussion (12:50–13:15, 25 min)
- Erfahrungsaustausch & Anwendungsfälle aus Teilnehmenden-Perspektive.
- Wo größte Skepsis / größtes Potenzial? (Moderationsfrage).
- Wrap-up: Takeaway-Material, Links (OpenCode, OpenSpec, SAIA, OpenDesk Edu).

---

## Puffer & Fallback-Strategie

| Situation | Reaktion |
|-----------|----------|
| Live-Demos scheitern | Vorab aufgenommene Videos (5–8 min) abspielen; Backup-Folien |
| Zeit knapp bei 3h-Format | Block 4 (−5 min) und Block 5 (entfällt/split) streichen; F & 6 geschützt |
| Block läuft über | Solche kürzen, was von Block 4/5 übrig ist |
| Hands-on-Block (F) zu lang | Auf 30 min komprimieren (Coding-Übung kürzen; Literature Review bleibt) |
| Q&A zieht nach | Diskussion läuft in die Pause bzw. offiziellen Rahmen über |

**Harte Prior-Tabelle (falls Gesamt zeit knapp):**
1. Block F (Hands-on) + Block 6 (OpenDesk) — höchster Schutz
2. Block 2 (Toolbox) + Block 3 (Vergleich)
3. Block 1 (SpecDriven) — Grundlage
4. Block 4/5 — flexibel kürzen / entfallen

---

## Optionale weitere Blöcke (falls Format weiter erweitert wird)

> Ergänzbare, eigenständig lauffähige Blöcke für ein Tagesseminar. Empfehlungen im Kontext der roten Linie „Agentic Engineering“.

| # | Block | Dauer | Für wen/Warum | Aufwand | Empfehlung |
|---|-------|-------|---------------|---------|------------|
| A | **Sicherheit & Governance** — Prompt-Injection, Supply-Chain (SBOM), Secrets, EU AI Act, DSGVO | 30 min | Compliance-lastige Forschungseinrichtungen; Top-Sorge bei Admins | mittel | ⭐⭐⭐ |
| B | **Evaluierung & QA für Agenten** — Eval-Sets, Test-Strategien, CI/CD, Sandboxing | 30 min | Antwortet auf „Halluzinationen“ — zeigt, wie man testet | mittel | ⭐⭐⭐ |
| C | **MCP & Standardisierung** — Model Context Protocol, Tool-Registry, Agent-zu-Agent-Schnittstellen | 20 min | Zukunftsthema; verbindet Modelle & Infrastruktur | gering | ⭐⭐⭐ |
| D | **Lokale & souveräne Modelle in der Forschung** — Ollama, vLLM, RAG, Knowledge Graphs | 30 min | IT4Science-Kernkompetenz; Daten verlassen nicht das Haus | mittel | ⭐⭐ |
| E | **Multi-Agent-Systeme & Orchestrierung** — Rollenverteilung, Delegation, Human-in-the-Loop | 30 min | Nächster Schritt nach Einzel-Agenten | mittel | ⭐⭐ |
| G | **Kosten & Betriebswirtschaft** — Token-Kosten, Model-Routing, Budgetierung, OS vs. API | 20 min | Für Entscheider im Publikum; konkreter Hebel | gering | ⭐⭐ |
| H | **Organisationstransformation** — Teams auf agentisches Arbeiten umstellen (Change-Management, Rollen, Schulungen) | 20 min | Beantwortet „wie fange ich an“ | gering | ⭐⭐ |
| I | **RAG & Wissensintegration** — Vektordatenbanken, Retrieval, Forschungs- /Organisationswissen | 30 min | Direkt anwendbar für alle mit Dokumentbeständen | mittel | ⭐⭐ |
| J | **Observability & Reliability von Agenten** — Monitoring, Tracing, Fehlerbehandlung, Selbstheilung | 20 min | Schlägt Brücke zum OpenDesk-Betrieb-Teil | gering | ⭐ |

> **Hinweis:** Block **F (Hands-on)** wurde in den Hauptplan übernommen und ist dort nicht mehr als „optional“ geführt (siehe oben).
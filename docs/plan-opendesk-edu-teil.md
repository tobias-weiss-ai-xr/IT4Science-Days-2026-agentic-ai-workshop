# Workshop-Teil: Use Case OpenDesk Edu — detaillierter Plan

> **Kontext:** IT4Science Days 2026 · Agentic AI Workshop (3h, Deutsch)
> **Agenda-Punkt:** *Use Case: OpenDesk Edu — Kollaborations-, Lern- und Forschungsplattform als praktisches Beispiel für Agentic Engineering*
> **Referenten:** Christian Uhl (Universität Gießen) · Tobias Weiß (Universität Marburg)
> **Dauer des Teils:** ~30 Minuten (inkl. Live-Demos, ohne Abschluss-Diskussion)

---

## 1. Leitgedanke

**Dieser Teil ist keine Produktpräsentation von openDesk, sondern eine Fallstudie über agentisches Entwickeln.**

Die Kernbotschaft: *Wie baut man eine Plattform mit 25+ integrierten Diensten (LMS, Sci-Computing, Groupware, Kollaboration), SSO überall, Backups, Monitoring und Produktionsreife — mit einem kleinen Team? Antwort: durch Spec-driven Development, agentische Implementierung und einen kontinuierlichen Self-Improvement-Loop.*

Am Ende soll das Publikum mitnehmen:

1. **Specs sind der Vertrag zwischen Mensch und Agent** — Delta-Specs (OpenSpec) ersetzen Klärungsrunden und machen Scope überprüfbar.
2. **Agenten können echte Produktionsarbeit leisten** — Helm-Charts, SSO-Integrationen, Tests, Betriebsfixes; mit Nachweis (44 Keycloak-Clients auditiert, 33/33 Services mit SSO, 97/97 Pods laufen).
3. **Der Betrieb lernt mit** — Knowledge Graph, Experience-Memory, Monitoring und der Ralph-Loop als "Continuous Self-Improvement".
4. **Übertragbarkeit** — Das Muster (Spec → Change → Agent → Review → Betrieb) funktioniert auch in kleineren Projekten; Tooling: OpenCode, OpenSpec, SAIA Accelerator.

**Abgrenzung zur CLT-2026-Präsentation:** Dort stand Souveränität im Vordergrund. Hier wird Souveränität nur als Motivation kurz angerissen; der Fokus liegt auf dem *agentic Engineering Workflow*.

---

## 2. Zeitplan im Detail (30 min)

| # | Zeit | Abschnitt | Dauer |
|---|------|-----------|-------|
| 1 | 00:00–02:00 | Einstieg: Frage ans Publikum + Warum OpenDesk Edu? | 2 min |
| 2 | 02:00–07:00 | Die Plattform in 5 Minuten (Demo: Portal, Landscape, Service-Matrix) | 5 min |
| 3 | 07:00–17:00 | **Agentic Engineering Showcase** — vom Change-Proposal zum deployed Service | 10 min |
| 4 | 17:00–24:00 | Live-Demo: SSO-Flow + Betrieb (Grafana, Backups, Cluster-Status) | 7 min |
| 5 | 24:00–28:00 | Lessons Learned & Zahlen, die beeindrucken | 4 min |
| 6 | 28:00–30:00 | Takeaway: Das Muster auf eigene Projekte übertragen | 2 min |

**Rahmenbedingungen / Fallbacks:**
- Live-Demos sind optional. Falls Live-Zugriff nicht klappt: vorab aufgenommene Screen-Capture-Videos (5–8 min) abspielen.
- Backup-Folien mit allen Screenshots (Portal, Landscape, Grafana, Cluster-Status) vorbereiten.
- Bei Zeitnot: Abschnitte 2 & 4 komprimieren; Abschnitt 3 ist der Kern und darf nicht gekürzt werden.

---

## 3. Abschnitt 1 — Einstieg & Motivation (00:00–02:00)

### Folie 1.1: Einstiegsfrage (Publikumsinteraktion)
> "Wie viele von Ihnen haben schon einmal ein Helm-Chart geschrieben? Einen SAML-SP integriert? Ein eigenes Open-Source-Produktivsystem betrieben?"

- Handzeichen → Bezug herstellen: OpenDesk Edu kombiniert *alle drei* — und genau das ist der Grund, warum agentisches Arbeiten hier so viel bringt.

### Folie 1.2: Warum OpenDesk Edu als Fallbeispiel? (Sprechzettel)
- openDesk CE ist die **BSI-zertifizierte, souveräne M365-Alternative** des Bundes (ZenDiS/BMI) — Kubernetes-basiert, modulare Komponenten (Element, Nextcloud, XWiki, OpenProject, OX, Collabora, Jitsi, CryptPad).
- Hochschulen brauchen **mehr**: LMS (ILIAS, Moodle), wissenschaftliches Rechnen (JupyterHub, Overleaf, RStudio, Dask), Lehre-Videokonferenz (BigBlueButton), lokale KI (Open WebUI + Ollama), Cloud-IDE (code-server), Web-Terminal (ttyd), Präsentationen (Slidev).
- Ergebnis: **openDesk Edu = openDesk CE + 25 Bildungs- & Forschungsdienste**, ein Deployment, ein Login (Keycloak), ein Backup-System (k8up).
- Der Clou für diesen Workshop: Eine solche Plattform *ohne* Agenten aufzubauen, wäre mit kleinem Team nicht in dieser Breite machbar.

---

## 4. Abschnitt 2 — Die Plattform in 5 Minuten (02:00–07:00)

### Folie 2.1: Ein Befehl, eine Plattform (Code-Folie)
```bash
git clone https://github.com/opendesk-edu/opendesk-edu.git
cd opendesk-edu
# Domain + Registry konfigurieren: helmfile/environments/default/global.yaml.gotmpl
helmfile -e default apply
```
- Kernaussage: Alles ist **deklarativ** — das ist die Voraussetzung dafür, dass Agenten sicher daran arbeiten können.

### Folie 2.2: Service-Matrix (kompakte Tabelle)
| Funktion | Dienste | Status |
|----------|---------|--------|
| Learning Management | ILIAS, Moodle | Stable/Beta |
| Sci-Computing | JupyterHub, Overleaf, RStudio, Dask Gateway, code-server, ttyd | Stable/Beta/Planned |
| KI lokal | Open WebUI + Ollama (llama3, mistral) | Stable/Beta |
| Lehre-Video | BigBlueButton (↔ Jitsi) | Beta |
| Kollaboration | Etherpad, BookStack, Planka, Draw.io, Excalidraw, TYPO3 | Beta/Stable |
| Support | Zammad, LimeSurvey, LTB Self-Service-Password | Beta/Stable |
| Alternative Komponenten | OX ↔ SOGo ↔ Grommunio, Nextcloud ↔ OpenCloud | wählbar |

### Folie 2.3: Demo — Live-Umgebung (wenn erreichbar)
- **Portal** (Nubus): alle Kacheln, ein Login.
- **Landscape** (landscape.opendesk-edu.org): interaktive Karte, Filter nach Kategorie, zeigt 80+ dokumentierte Service-Beziehungen.
- **Collab-Services** unter eigenem Subdomain-Bereich.
- Sprechzettel: "Was Sie hier sehen, ist nicht konfiguriert, sondern *spezifiziert* — und genau das macht es agenten-tauglich."

---

## 5. Abschnitt 3 — Agentic Engineering Showcase (07:00–17:00) ⭐ Kern des Teils

**Storyline:** Idee → Spec → Agent implementiert → Test → Merge → im Betrieb. An realen Artefakten aus dem Repo zeigen.

### 5.1 Der Workflow (Folie 3.1, 2 min)

```
Idee / Ticket
   │
   ▼
┌─────────────────────────────────────────────┐
│ OpenSpec Change (changes/<name>/)           │
│   proposal.md  → Was & warum                │
│   specs.md     → Delta-Specs (ADDED/…)      │
│   tasks.md     → Implementierungsschritte   │
└─────────────────────────────────────────────┘
   │   Delta-Spec = Prompt für den Agenten
   ▼
┌─────────────────────────────────────────────┐
│ Agent (OpenCode + SAIA Accelerator)         │
│   implementiert Helm-Chart, Values, SSO,    │
│   Tests — in kleinen, verifizierbaren Steps │
└─────────────────────────────────────────────┘
   │
   ▼
Review → Tests (pytest, Playwright) → Merge → helmfile apply
   │
   ▼
Betrieb: Monitoring, Backups, Ralph-Loop (Lessons → Specs → nächster Change)
```

**Kernaussagen:**
- `specs/` = Source of Truth (behaviorale Verträge, Given/When/Then, SHALL/MUST/SHOULD).
- `changes/` = Delta-Specs; der Agent bekommt exakt die Differenz — **keine Klärungsfragen nötig, Scope klar prüfbar**.
- `archive/` = Decision Log — "warum ist TYPO3 per OIDC angebunden?" ist in 6 Monaten noch beantwortbar.
- STATE.md pro Projektphase ersetzt das Neuerklären in jeder Agent-Session (Per-Phase Context Management).

### 5.2 Live am Beispiel: eine echte SSO-Integration (Folie 3.2, 4 min)

**Fallbeispiel ILIAS (aus den echten Lessons Learned):** ILIAS + Shibboleth SP + Keycloak-Broker gegen Uni-IdP.

Zeigen:
1. Den Change-Ordner mit `proposal.md` / `specs.md` / `tasks.md` (aus `opendesk-edu-spec/changes/`).
2. Einen Auszug aus der Delta-Spec für ILIAS (SAML).
3. Das Ergebnis: 6-Schritt-SSO-Flow (Portal → ILIAS → Shibboleth SP → Keycloak → Uni-IdP → Dashboard).

**Die echten Fehler & Fixes als Story (Tabellen-Folie, Gold wert fürs Publikum):**

| Problem beim Deployment | Lösung durch Agent + Review |
|---|---|
| `Wrong Login or Password` | SAML `NameFormat` fehlte in `attribute-map.xml` |
| Attribute kamen nicht an | Uni-IdP sendet `givenname`/`surname` → Mapping korrigiert |
| `handlerSSL` → 404 | Internes TLS: Apache SSL auf Port 8443 |
| Accounts sofort deaktiviert | `shib_activate_new = 0` |
| SAML-Timeout | 60 s → 300 s |
| Fehler blieben unbemerkt | CronJob-HealthCheck: curl SSO-Redirect stündlich |

**Botschaft:** Agenten beschleunigen, aber die *Verifikation* (Tests, HealthChecks, Review) ist der eigentliche Qualitätshebel. Agenten liefern nicht "auf Knopfdruck perfekt", sondern machen das iterative Fixen viel schneller.

### 5.3 Skalierung: von einem Service zu 25 (Folie 3.3, 3 min)

- **Muster wiederverwenden:** Jeder Service ist ein eigenes Helm-Chart mit identischem Skelett (Values-Templates, Ingress, SSO-Anbindung, Tests) — Chart-Scaffolding per Agent in "Waves" parallelisiert.
- **Integrations-Contract:** `opendesk_core.schema.json` + API-Contracts → Agenten bekommen die Schnittstellenbeschreibung, statt sie zu erraten.
- **SSO-Audit:** 44 Keycloak-Clients, 33/33 Services mit SSO, alle URIs auf `*.home.opendesk-edu.org` verifiziert — als agentisch erzeugter Prüfbericht (COMPLIANCE-REPORT).
- **Test-Mapping & Interconnection-Matrix** im `_registry/` — jede Spec ist mit Tests verknüpft.

### 5.4 Der Self-Improvement-Loop (Folie 3.4, 3 min)

- **Ralph-Loop** (`specs/automation/ralph-loop/`): kontinuierlicher Verbesserungszyklus — Betriebserkenntnisse werden zu Spec-Änderungen, Spec-Änderungen zu Changes, Changes zu Implementierung.
- **opendesk-dev-agent** (Zot-Extension): Slash-Commands wie `/opendesk-find`, `/opendesk-status`, `/opendesk-learn`; Knowledge Graph (Neo4j) + Experience-Memory (pi-memory) → das Wissen wächst mit jeder Session (Kategorien: insight / decision / pattern / warning / todo).
- **Betrieb als Feedback:** Grafana-Dashboards (edu-health, k8up), Backup-Schedules, ArgoCD → Fehler aus der Produktion werden zu nächsten Changes.
- **Veröffentlichung als Nebeneffekt:** Specs → Docusaurus-Doku, Artikel (de/en/fr/zh), Präsentationen in 30 Sprachen — *agentisch generiert und geprüft*.

---

## 6. Abschnitt 4 — Live-Demo: Betrieb (17:00–24:00)

### Demo A (3 min): SSO-Ende-zu-Ende
1. Portal öffnen → ILIAS-Kachel → automatischer Redirect → Uni-IdP-Login → Dashboard.
2. Kurz zeigen: ein zweiter Dienst (z. B. Overleaf oder JupyterHub) ohne erneuten Login.

### Demo B (2 min): Cluster & Betrieb
```bash
kubectl get pods -n opendesk | grep -c Running    # z. B. 97/97
kubectl get cronjob -n opendesk -l app.kubernetes.io/component=backup
kubectl get ingress -n opendesk | wc -l
```
- Grafana öffnen: edu-health Dashboard, k8up-Backup-Status, Service-Uptime.
- Botschaft: "Was Agenten gebaut haben, ist auch *agentisch überwachbar* — Statusabfragen sind Teil des Workflows (siehe `/opendesk-status`)."

### Demo C (2 min, wenn Zeit): Ein Change in Aktion
- Kleinen Beispiel-Change zeigen: `helmfile diff -e production` vor/nach einer Values-Änderung.
- Oder: Agent eine Mini-Aufgabe geben lassen (z. B. "Finde den Ingress ohne korrekte Ingress-Class" → `/opendesk-find`), um zu zeigen, wie der Agent im Projekt navigiert.

---

## 7. Abschnitt 5 — Lessons Learned & Zahlen (24:00–28:00)

### Folie: Was hat agentisches Arbeiten gebracht?
| Bereich | Nachweis |
|---|---|
| Breite | 25+ zusätzliche Dienste in wenigen Monaten (statt Jahren) |
| Konsistenz | 44/44 Keycloak-Clients auditiert, 33/33 Services SSO, 33 Ingresses korrekt |
| Betrieb | 97/97 Pods laufen, 5 Backup-CronJobs aktiv, 14d Retention |
| Wissen | 56 Specs (24 Services, 17 Platform, 4 Auth, 6 Integrations, 5 Registry) |
| Qualität | pytest-Integrationstests + Playwright-E2E (Backchannel, SAML-Metadaten, Semester-Lebenszyklus) |

### Folie: Ehrliche Hürden (wichtig für Glaubwürdigkeit)
- **Institutionell > technisch:** Rechtsabteilung (DSGVO, AVV), Personalrat (Dienstvereinbarung), Verwaltung (Microsoft-Präferenzen); DSFA + TCO-Kalkulation nötig.
- **Agenten-Halluzinationen & Config-Fehler:** nur durch Tests, HealthChecks und Review abzufangen — Agenten sind *beschleunigende* Mitarbeiter, keine Ersatz-Reviews.
- **Upstream-Drift:** Charts basieren auf Upstream-Images; eigenes Image-Building & Security-Patching ist Roadmap-Thema (Souveränität).
- **Ops-Wissen bleibt nötig:** Kubernetes, Keycloak, Helm/helmfile, SAML/OIDC — Agenten helfen, aber ein Mensch muss das Betriebsmodell verantworten.

### Folie: Kennzahlen des realen Clusters
- K3s v1.32.3 · Debian 12 · 9 Knoten (3 CP + 6 Worker) · 16+ Kerne · 64+ GB RAM · 4+ TB Ceph.
- Ingress: haproxy-ingress (migriert von nginx), Traefik-Reverse-Proxy, MetalLB.
- SSO: Keycloak (SAML2 + OIDC), Shibboleth SP für ILIAS/Moodle/BBB, DFN-AAI/eduGAIN-Föderation.
- Pilotierung UMR: 3 Stufen (HRZ/IT → Verwaltung → Fachbereiche), 24–36 Wochen, mit Checklisten & DR-Plan.

---

## 8. Abschnitt 6 — Takeaway & Übertragbarkeit (28:00–30:00)

### Folie: Das Muster auf eigene Projekte übertragen
1. **Klein starten:** Eine Spec für ein vorhandenes Modul schreiben (Given/When/Then).
2. **Delta-Specs nutzen:** Ersten Change mit 3 Tasks formulieren → Agent (OpenCode) implementieren lassen.
3. **Verifikation erzwingen:** Tests + Review als *Pflicht-Schritt* definieren; Agenten-Fixes iterieren lassen.
4. **Wissen persistieren:** pi-memory/Knowledge-Graph ab Session 1; STATE.md für Multi-Session-Projekte.
5. **Loop institutionalisieren:** Betriebserkenntnisse werden Changes (Ralph-Loop).

### Folie: Tools & Links (Abschlussfolie)
- **OpenCode** — offener agentischer Coding-Terminal: github.com/sst/opencode
- **OpenSpec** — Spec-driven Development: github.com/Fission-AI/OpenSpec (bzw. FissionAI/OpenSpec)
- **SAIA Accelerator** — Plugin für OpenCode: codeberg.org/graphwiz-ai/opencode-saia-plugin
- **openDesk Edu:** github.com/opendesk-edu/opendesk-edu · opendesk-edu.org · landscape.opendesk-edu.org
- **Spec-Repo:** github.com/opendesk-edu/opendesk-edu-spec
- **Artikel:** "The openDesk Edu Platform", "Extending Intercom Service", "OpenSpec digital sovereign workplace" (de/en/fr/zh)

### Überleitung zur Abschluss-Diskussion (1 Satz)
> "OpenDesk Edu zeigt: Mit Specs als Vertrag und Agenten als Team kann ein kleines Team eine große, produktionsreife Plattform aufbauen. Jetzt zu Ihnen: Wo sehen Sie das größte Potenzial — und wo die größte Skepsis, Agenten produktiven Code schreiben zu lassen?"

---

## 9. Vorbereitung & Technik-Checkliste

- [ ] Live-Cluster-Zugriff getestet (VPN/Proxy; alternativ: Screen-Capture-Videos 5–8 min bereitlegen)
- [ ] Portal-Login-Demo-Accounts bereit (Keycloak + ILIAS + ein Sci-Computing-Dienst)
- [ ] Terminal-Konfiguration: `kubectl` gegen Produktionscluster, `helmfile diff` vorgeladen
- [ ] Landscape-URL offline-tauglich? Sonst Screenshot-Folie
- [ ] Folien aus `opendesk-edu/docs/pr/linuxtag-2026/linuxtag-2026-opendesk.md` übernehmen (Assets: proxmox.png, grafana.png, ilias-gif, readme-lead-image.svg)
- [ ] Projektor-Auflösung: Grafana/Portal-Tabs im Voraus geöffnet, Fenstergrößen vorkonfiguriert
- [ ] Backup-Folien: Cluster-Status, COMPLIANCE-REPORT-Auszug, Zahlen-Tabelle

---

## 10. Referenzen (Quellenmaterial im Monorepo)

| Inhalt | Pfad |
|---|---|
| Projekt-README (Komponenten, Status, Zahlen) | `opendesk-edu/README.md` |
| Spec-Framework & Methodik | `opendesk-edu-spec/README.md`, `METHODOLOGY.md` |
| Ralph-Loop | `opendesk-edu-spec/specs/automation/ralph-loop/index.md` |
| Dev-Agent (Zot, KB, pi-memory) | `opendesk-dev-agent/README.md` |
| ILIAS-Lessons & SSO | `opendesk-edu/docs/ilias-shibboleth-attribute-fix.md`, Präsentation CLT 2026 |
| Betriebsstatus | `CURRENT-ACTIONS.md`, `FINAL-CLUSTER-STATUS.md`, `TASK-COMPLETION-SUMMARY.md` |
| Pilotierung UMR | `erprobungskonzept/pilotierungsplan.md` |
| Artikel | `opendesk-edu/articles/` (platform-overview, openspec-digital-sovereign-workplace, intercom, sops) |
| CLT-2026-Präsentation (Folien-Quelle) | `opendesk-edu/docs/pr/linuxtag-2026/linuxtag-2026-opendesk.md` |

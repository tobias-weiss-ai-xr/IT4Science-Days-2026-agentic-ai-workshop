---
marp: true
theme: default
paginate: true
footer: 'GöAID · Agentic AI in Practice · openedusuite.graphwiz.ai'
style: |
  section {
    background-color: #1a1a1a;
    color: #e8e8e8;
    font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    padding-bottom: 64px;
  }
  section.smaller table { font-size: 18px; }
  section.smaller table th, section.smaller table td { padding: 4px 8px; }
  h1, h2, h3 { color: #ffffff; font-weight: 700; }
  table { margin: 0 auto; font-size: 22px; border-collapse: collapse; }
  table th, table td {
    background-color: #2a2a2a; padding: 6px 11px;
    border: 1px solid #555; color: #e8e8e8;
  }
  table thead th {
    background-color: #383838; color: #ffffff; border-bottom: 2px solid #666;
  }
  table tbody tr:nth-child(even) td { background-color: #252525; }
  pre {
    background: #111; border: 1px solid #444; border-radius: 6px;
    color: #d8d8d8; font-size: 20px;
  }
  blockquote {
    border-left: 4px solid #3b6fc4; color: #c8d8f0;
    font-style: italic; font-size: 24px;
  }
---

<!-- _class: lead -->

# Agentic AI in Practice

## From Spec to Productive Workflow

Tobias Weiß · DevOps, Universität Marburg

GöAID Session · Academic Cloud

<!-- notes:
(1 min) Begrüßung. Satz 1: Ich zeige heute keinen Vortrag ÜBER Agenten,
sondern einen Betrieb, der VON Agenten gebaut und gefahren wird.
30 min Inhalt + 10 min Fragen. Sprache: Deutsch, Begriffe Englisch.
-->

---

## Wo ich herkomme: ein Betrieb, kein Labor

- openEduSuite: souveräne Groupware-Suite für Lehre, Forschung, Verwaltung — auf Bare-Metal-Kubernetes.
- **AI-infused** heißt bei uns zweierlei: LLM-Dienste *in* der Suite und Agenten *am* Betrieb der Suite.
- Produktion, keine Demo: echte Postfächer, echte Studierende, echte Ausfälle.

> Diese Session ist die Geschichte, wie aus Specs produktive Workflows wurden.

<!-- notes:
(2 min) Kontext setzen: Uni Marburg, DevOps. Die Suite läuft produktiv
auf eigenen Bare-Metal-Nodes (SCS-K8s), nicht in einer Public Cloud.
Zwei Richtungen von "AI-infused": (a) die Suite trägt eigene LLM-/K8s-
Ressourcen (k8s/llm), (b) der Betrieb selbst wird agentisch gemacht.
Letzteres ist der Stoff dieses Vortrags.
-->

---

<!-- _class: smaller -->

## Fahrplan — 30 Minuten, drei Blöcke

| Block | Inhalt | Zeit |
|---|---|---|
| 1 · Grundlagen | Was „agentisch" konkret heißt: Modell + Harness + Schleife | ~8 min |
| 2 · Methode | Spec → Contract → Agent → Verify: die Pipeline | ~10 min |
| 3 · Praxis | Vier Fälle aus dem openEduSuite-Betrieb | ~12 min |

Danach: **10 Minuten Fragen.**

<!-- notes:
(30 s) Nur zeigen, nicht vorlesen. Block 3 ist das Herz — die vier
Fälle sind echte Incidents/Projekte mit Datum und Ergebnis.
-->

---

## Agentisch ≠ Chat

- Chat: Frage → Antwort. Agent: **Ziel → Plan → Werkzeuge → Ergebnis → Rückmeldung.**
- Drei Bausteine: Modell + Werkzeuge (Terminal, Dateien, Git, Cluster) + Schleife (planen, ausführen, prüfen).
- Der Unterschied sitzt nicht im Modell — sondern im **Harness** drumherum.

> „Agentic" ist kein Modell-Feature, sondern eine Arbeitsumgebung.

<!-- notes:
(2 min) Erwartungsmanagement: Agenten sind keine fertigen Bots.
Ein Modell im Chat-Fenster kann keine Datei anfassen. Der Agent =
Modell im Rahmen, der ihm Werkzeuge und Regeln gibt.
Erfahrung aus unseren Kursen (JLU-Feedback): Viele erwarten "fertige
Bots" — diesen Begriff hier sauber setzen.
-->

---

## Das Harness bestimmt, was das Modell erreichen kann

- Gleiches Modell, anderer Rahmen: Chat-Fenster vs. Terminal-Agent mit Datei-, Git- und Cluster-Zugriff.
- Unser Harness: **pi** — Terminal-Agent, MCP-Werkzeuge, Skills, Speicher über Sitzungen hinweg.
- **Plan-Mode:** erst lesen und planen, dann schreiben — der Agent zeigt den Plan, bevor er greift.

> Was der Agent darf, steht im Contract — nicht im Bauchgefühl.

<!-- notes:
(2 min) pi kurz zeigen oder beschreiben: öffnet Terminals, liest
Dateien, führt Git aus, ruft MCP-Tools auf. Plan-Mode = Einwilligung
vor jeder Änderung. Wichtig fürs Publikum aus dem Betrieb: der Agent
hat dieselben Rechte wie ich am Arbeitsplatz — deshalb Contract.
-->

---

## Die Pyramide: Spec · Contract · Test

- **Spec** — WAS soll gebaut werden: Anforderung + Akzeptanzkriterien.
- **Contract** — WORAN orientiert sich der Agent: `AGENTS.md`, Repo-Konventionen, Grenzen.
- **Test** — WANN ist es richtig: CI, e2e-Suiten, Footer-Checks.

> Jede Stufe ist Text im Repo — damit wird die Arbeit wiederholbar statt heldenhaft.

<!-- notes:
(2 min) Kernfolie der Methode. Die drei Ebenen liegen alle im
Git-Repo, nicht in Köpfen oder Chats. Überleitung: "Wie kommt man von
dieser Pyramide zu einem laufenden Workflow? → OpenSpec."
-->

---

## Von der Spec zum Change: OpenSpec

- Ein **Change** = proposal + spec-delta + tasks — versioniert im Repo, für Mensch *und* Agent lesbar.
- Der Agent implementiert Task für Task; der Mensch reviewt und **archiviert**.
- Archiviert heißt: die Spec im main-Zweig ist der neue Stand — **Dokumentation ist das Produkt**, kein Nebenprodukt.

```text
Spec (OpenSpec) → Contract (AGENTS.md) → Agent (pi)
      → Verify (Tests/CI) → Operate (ArgoCD)
```

<!-- notes:
(2 min) OpenSpec-Kommandozeile: new change, continue, apply, archive.
Der Ablauf: proposal von Mensch oder Agent, Verfeinerung im Dialog,
dann tasks abarbeiten. Wichtig: "archive" aktualisiert die Specs —
so bleibt die Doku synchron mit dem System.
-->

---

<!-- _class: smaller -->

## Bühne: openEduSuite in einem Slide

| Baustein | Dienst | | Baustein | Dienst |
|---|---|---|---|---|
| Identität | **Keycloak** (SSO) | | Chat | **Matrix/Synapse** |
| Groupware | **SOGo** | | Projekte | **OpenProject** |
| Files | **OpenCloud** | | Video | **Jitsi/Intercom** |
| Wiki | **XWiki** | | Portal | **collab-dashboard** |

- GitOps: **ArgoCD** reconciliert den Cluster; Bare-Metal (SCS), MariaDB/Galera, HAProxy.
- Agenten arbeiten hier am Produktivsystem — deshalb: **Spec vor Ausführung, Test als Abnahme.**

<!-- notes:
(2 min) Publikum verorten: Wer betreibt sowas ähnliches, kennt die
Bausteine. Ein Login, acht Dienste. Der untere Bullet ist die
Kernspannung des Vortrags: Agenten mit Schreibrechten am
Produktivsystem — wie macht man das verantwortbar? Antwort: die
nächsten vier Fälle.
-->

---

## Fall 1 · Domain-Wechsel der ganzen Suite — als Spec

- Ausgangslage: Cutover `home.openedu` → `suite.graphwiz.ai` — Ingresses, Zertifikate, OAuth-Redirects, Mail-Domains im ganzen Stack.
- Mensch schreibt den **Vertrag**: Swap-Skript idempotent, Guard-Zähler (157 + 8 Manifeste dürfen *nicht* angefasst werden), Keycloak-Redirects, Let's-Encrypt-Wildcard.
- Agent implementiert `bootstrap-domain-swap.sh` — Prüfkriterien grün, erst dann Ausführung.

> Ein nervöser Cutover wird zur Routine: das Skript darf man einfach nochmal laufen lassen.

<!-- notes:
(3 min) Der Witz: ohne Spec wäre das eine Woche Handarbeit mit
Angst. Mit Spec: ein Skript mit eingebauten Guards. Idempotenz ist
das Abnahmekriterium — zweites Laufen ändert nichts. Story: beim
ersten Lauf flog die Guard-Prüfung an (ein Verzeichnis zu viel
gematcht) — genau dafür sind Guards da.
-->

---

## Fall 2 · SSO-Rätsel: weiße Seite nach dem Login

- Symptom: SOGo-Webmail zeigt nach SAML-Login eine **weiße Seite** — drei Ursachen hintereinander.
- Agent im Plan-Mode: Hypothesen → Probes (Metadata-Dump, ACS-URL, TLS-Hop am Ingress) → Fix → Test.
- Zweitfall gleiches Muster: Stalwart-XOAUTH2 brach an einem toten OIDC-Issuer in einem Directory-Objekt.

> Debugging ist der beste Agenten-Fall: Symptom rein, Ursachenkette raus — mit Protokoll zum Nachlesen.

<!-- notes:
(3 min) live erzählen, das publikum kennt weiße seiten. Punkt 1:
Repo/Deploy hingen noch an alten Domains + Platzhalter-IdP-Metadaten.
Punkt 2: TLS-Terminierung am Ingress vs. ACS-URL-Schema. Der Agent
brauchte mehrere Probes — aber jede Hypothese war sichtbar. Danach
wurde die Ursache jeweils zur Probe in der Testsuite. Merksatz:
"Jeder gefundene Fehler wird ein Test, bevor er wiederkommt."
-->

---

## Fall 3 · „Fix-All": Drift sichtbar machen

- Muster: k8s-Verzeichnisse, die **kein** ArgoCD-App hatte — Tenant-Mail, LLM, XWiki; Erbe aus der imperativen Apply-Ära.
- Aufträge mit Abnahmekriterien: jede App unter GitOps, jeder Diff erklärt, nichts implizit.
- Nebenbefund: `k8s/llm` — der Modellbetrieb ist Teil derselben Suite.

> Agenten sind gut im Kleinarbeiten ganzer Verzeichnisse — wenn die Definition of Done im Vertrag steht.

<!-- notes:
(2 min) Diese Art Arbeit ist langweilig und wichtig — perfekt für
Agenten. Mensch definiert: was ist "fertig"? (App existiert, Sync
grün, kein unmanaged Manifest mehr.) Der Agent arbeitet die Liste
ab. Botschaft an das Publikum:fangen Sie mit so Aufgaben an, nicht
mit "schreib meine Bewerbung".
-->

---

## Fall 4 · Agenten-Fleet mit Acceptance-Gates

- Die SSO-Testsuite (**59 Checks, 15 Clients e2e**) entstand in Batches: parallele Worker, isolierte Git-Worktrees.
- Jeder Task hatte exakte Akzeptanzkriterien; Merge erst nach grün — sonst verwirft der Fleet-Runner.
- Fleet = Spec in der Breite: einmal Verträge schreiben, viele kleine Aufträge verteilen.

> Nicht ein Super-Agent — viele kleine Aufträge mit Tests. Skalierbar, billig, nachvollziehbar.

<!-- notes:
(3 min) taskfleet: tasks.json + workers.json, isolierte Worktrees,
automatischer Merge nur bei grünen Gates. Damit wurden die e2e-Checks
für alle SSO-Clients gebaut — Logout je Client-Typ, Session-TTL,
Scopes. Ein Mensch hätte da wochenlang geklickt.
-->

---

## Was der Betrieb daraus gelernt hat

- **Enge Specs statt große Kontexte:** weniger Token, gleiche Qualität — die Spec ist der Kompressor.
- **Erwartungen steuern:** Agenten liefern keine fertigen Bots — sie brauchen Contract und Tests.
- **Test zuerst:** jeder Incident wird ein Test. Jede Warnung in der Suite ist ein dokumentierter Beschluss.

> Vertrauen ist gut. Verification ist billiger.

<!-- notes:
(2 min) Die drei Lektionen sind bewusst betriebsnah formuliert.
Token-Fall: Eine enge Spec mit 5 Akzeptanzkriterien schlägt einen
1000-Zeilen-Prompt. Erwartungen: aus unseren Workshops — Menschen
wollen "fertige Bots", bekommen ein Werkzeug mit Regeln. Test
zuerst: die SSO-Suite ist genau so entstanden (59/0/6, jede Warnung
besprochen).
-->

---

## Das Muster auf Ihr Projekt übertragen

1. **Contract zuerst:** `AGENTS.md` im Repo — was darf der Agent, wo liegen die Fakten.
2. **Spec-Change vor Code:** Aufgaben klein, mit Akzeptanzkriterien — proposal → tasks → apply → archive.
3. **CI ist die Abnahme:** grün = fertig. Der Agent darf wiederholen, Sie prüfen das Ergebnis.
4. **Speicher über Sitzungen:** Entscheidungen landen im Repo und im Memory — nicht im Chat-Verlauf.

> Fangen Sie mit einer langweiligen, wichtigen Aufgabe an. Nicht mit dem Selbstversuch „Agent ersetzt mich".

<!-- notes:
(2 min) Die Übertragungs-Folie: das Publikum soll morgen eine Sache
machen können. Punkt 1 kostet 20 Minuten und verändert alles — der
Agent liest den Contract bei jedem Start. Punkt 4: experiences /
Spec-Repo statt Chat-History.
-->

---

## Resources

- **openEduSuite** — `openedusuite.graphwiz.ai` · Portal: `openedu.graphwiz.ai`
- **Workshop-Repo** (IT4Science Days 2026, 3h-Deck + Übungen) — GitHub/Codeberg: `IT4Science-Days-2026-agentic-ai-workshop`
- **Werkzeuge:** pi (Terminal-Agent) · OpenSpec (Spec-Workflow) · taskfleet (Agenten-Fleet) · ArgoCD (GitOps)

Alles Greifbares: Repos, Specs, Testsuiten — keine Folien-Magie.

<!-- notes:
(30 s) Nicht vorlesen. Hinweis: der Workshop-Deck (3h-Version) ist
öffentlich — wer tiefer einsteigen will, macht die Übungen selbst.
-->

---

<!-- _class: lead -->

# Vielen Dank!

## Fragen? — 10 Minuten

Tobias Weiß · `tobias.weiss@uni-marburg.de`

GöAID · openEduSuite · Uni Marburg

<!-- notes:
(10 min) Q&A. Wahrscheinliche Fragen: Sicherheit/Rechte der Agenten
(→ Contract + Plan-Mode + Tests), Modellwahl (→ Harness unabhängig,
pi läuft mit verschiedenen Providern), Kosten (→ enge Specs, kleine
Aufträge), Einstieg (→ AGENTS.md + eine langweilige Aufgabe).
-->

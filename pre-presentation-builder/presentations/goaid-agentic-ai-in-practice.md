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

Tobias Weiß · DevOps, University of Marburg

GöAID Session · Academic Cloud

<!-- notes:
(1 min) Welcome. Sentence 1: This is not a talk ABOUT agents — it is
the story of an operation that is built and run BY agents.
30 min of content + 10 min of questions.
-->

---

## Where I come from: an operation, not a lab

- openEduSuite: sovereign groupware suite for teaching, research, administration — on bare-metal Kubernetes.
- **AI-infused** means two things here: LLM services *in* the suite, and agents working *on* the operation.
- Production, not a demo: real mailboxes, real students, real outages.

> This session is the story of how specs turned into productive workflows.

<!-- notes:
(2 min) Set the context: University of Marburg, DevOps. The suite runs
productively on our own bare-metal nodes (SCS-K8s), not in a public
cloud. Two directions of "AI-infused": (a) the suite carries its own
LLM/K8s resources (k8s/llm), (b) the operation itself is done
agentically — the latter is the subject of this talk.
-->

---

<!-- _class: smaller -->

## Roadmap — 30 minutes, three blocks

| Block | Content | Time |
|---|---|---|
| 1 · Foundations | What "agentic" concretely means: model + harness + loop | ~8 min |
| 2 · Method | Spec → Contract → Agent → Verify: the pipeline | ~10 min |
| 3 · Practice | Four cases from the openEduSuite operation | ~12 min |

Afterwards: **10 minutes of questions.**

<!-- notes:
(30 s) Show, don't read. Block 3 is the heart — the four cases are
real incidents/projects with dates and outcomes.
-->

---

## Agentic ≠ chat

- Chat: question → answer. Agent: **goal → plan → tools → result → feedback.**
- Three building blocks: model + tools (terminal, files, git, cluster) + loop (plan, act, verify).
- The difference does not live in the model — it lives in the **harness** around it.

> "Agentic" is not a model feature, it is a working environment.

<!-- notes:
(2 min) Expectation management: agents are not finished bots. A model
in a chat window cannot touch a file. The agent = model inside a frame
that gives it tools and rules. Lesson from our courses (participant
feedback): many expect "ready-made bots" — set that term straight here.
-->

---

## The harness determines what the model can achieve

- Same model, different frame: chat window vs. terminal agent with file, git and cluster access.
- Our harness: **pi** — terminal agent, MCP tools, skills, memory across sessions.
- **Plan mode:** read and plan first, write later — the agent shows the plan before it touches anything.

> What the agent may do is written in the contract — not left to gut feeling.

<!-- notes:
(2 min) Briefly show or describe pi: opens terminals, reads files,
runs git, calls MCP tools. Plan mode = consent before any change.
Important for the ops crowd: the agent has the same rights I have at
my workstation — hence the contract.
-->

---

## The pyramid: Spec · Contract · Test

- **Spec** — WHAT is to be built: requirement + acceptance criteria.
- **Contract** — WHAT the agent orients itself by: `AGENTS.md`, repo conventions, boundaries.
- **Test** — WHEN it is correct: CI, e2e suites, footer checks.

> Every level is text in the repo — that makes work repeatable instead of heroic.

<!-- notes:
(2 min) Core slide of the method. All three levels live in the git
repo, not in heads or chats. Transition: "How do you get from this
pyramid to a running workflow? → OpenSpec."
-->

---

## From spec to change: OpenSpec

- A **change** = proposal + spec delta + tasks — versioned in the repo, readable by human *and* agent.
- The agent implements task by task; the human reviews and **archives**.
- Archived means: the spec on main is the new state — **documentation is the product**, not a by-product.

```text
Spec (OpenSpec) → Contract (AGENTS.md) → Agent (pi)
      → Verify (tests/CI) → Operate (ArgoCD)
```

<!-- notes:
(2 min) OpenSpec CLI: new change, continue, apply, archive. The flow:
proposal by human or agent, refinement in dialogue, then work through
tasks. Key point: "archive" updates the specs — that is how the docs
stay in sync with the system.
-->

---

<!-- _class: smaller -->

## The stage: openEduSuite on one slide

| Component | Service | | Component | Service |
|---|---|---|---|---|
| Identity | **Keycloak** (SSO) | | Chat | **Matrix/Synapse** |
| Groupware | **SOGo** | | Projects | **OpenProject** |
| Files | **OpenCloud** | | Video | **Jitsi/Intercom** |
| Wiki | **XWiki** | | Portal | **collab-dashboard** |

- GitOps: **ArgoCD** reconciles the cluster; bare metal (SCS), MariaDB/Galera, HAProxy.
- Agents work on this production system — hence: **spec before execution, test as acceptance.**

<!-- notes:
(2 min) Locate the audience: anyone running something similar knows
these components. One login, eight services. The bottom bullet is the
core tension of this talk: agents with write access on production —
how do you make that accountable? Answer: the next four cases.
-->

---

## Case 1 · Domain migration of the whole suite — as a spec

- Starting point: cutover `home.openedu` → `suite.graphwiz.ai` — ingresses, certificates, OAuth redirects, mail domains across the whole stack.
- Human writes the **contract**: swap script idempotent, guard counters (157 + 8 manifests must *not* be touched), Keycloak redirects, Let's Encrypt wildcard.
- Agent implements `bootstrap-domain-swap.sh` — acceptance criteria green, only then execution.

> A nerve-racking cutover becomes routine: you can simply run the script again.

<!-- notes:
(3 min) The point: without a spec this is a week of manual work and
fear. With a spec: one script with built-in guards. Idempotency is
the acceptance criterion — a second run changes nothing. Story: on
the first run a guard check fired (one directory matched too much) —
exactly what guards are for.
-->

---

## Case 2 · SSO mystery: white page after login

- Symptom: SOGo webmail shows a **white page** after SAML login — three root causes in a row.
- Agent in plan mode: hypotheses → probes (metadata dump, ACS URL, TLS hop at the ingress) → fix → test.
- Second case, same pattern: Stalwart XOAUTH2 broke on a dead OIDC issuer inside a directory object.

> Debugging is the best agentic use case: symptom in, root-cause chain out — with a log you can reread.

<!-- notes:
(3 min) Tell it live; everyone knows white pages. Point 1: repo/deploy
still hung on old domains + placeholder IdP metadata (by design).
Point 2: TLS termination at the ingress vs. ACS-URL scheme. The agent
needed several probes — but every hypothesis was visible. Afterwards
each root cause became a probe in the test suite. Key line: "Every bug
found becomes a test before it comes back."
-->

---

## Case 3 · "Fix-all": making drift visible

- Pattern: k8s directories with **no** ArgoCD app — tenant mail, LLM, XWiki; legacy from the imperative-apply era.
- Orders with acceptance criteria: every app under GitOps, every diff explained, nothing implicit.
- Side finding: `k8s/llm` — the model serving is part of the same suite.

> Agents are great at the tedious work of whole directories — if the definition of done is in the contract.

<!-- notes:
(2 min) This kind of work is boring and important — perfect for
agents. The human defines: what is "done"? (App exists, sync green,
no unmanaged manifests left.) The agent works through the list.
Message to the audience: start with tasks like this, not with
"write my thesis".
-->

---

## Case 4 · An agent fleet with acceptance gates

- The SSO test suite (**59 checks, 15 clients e2e**) was built in batches: parallel workers, isolated git worktrees.
- Every task had exact acceptance criteria; merge only on green — otherwise the fleet runner discards it.
- Fleet = spec at scale: write contracts once, distribute many small orders.

> Not one super-agent — many small orders with tests. Scalable, cheap, auditable.

<!-- notes:
(3 min) taskfleet: tasks.json + workers.json, isolated worktrees,
automatic merge only with green gates. This is how the e2e checks for
all SSO clients were built — logout per client type, session TTL,
scopes. A human would have spent weeks clicking through this.
-->

---

## What the operation learned

- **Tight specs over big contexts:** fewer tokens, same quality — the spec is the compressor.
- **Manage expectations:** agents do not deliver finished bots — they need contracts and tests.
- **Test first:** every incident becomes a test. Every warning in the suite is a documented decision.

> Trust is good. Verification is cheaper.

<!-- notes:
(2 min) The three lessons are deliberately phrased for operations.
Token case: a tight spec with 5 acceptance criteria beats a
1000-line prompt. Expectations: from our workshops — people want
"finished bots" and get a tool with rules. Test first: the SSO suite
was built exactly this way (59/0/6, every warning discussed).
-->

---

## The pattern, applied to your project

1. **Contract first:** `AGENTS.md` in the repo — what the agent may do, where the facts live.
2. **Spec change before code:** small tasks with acceptance criteria — proposal → tasks → apply → archive.
3. **CI is the acceptance:** green = done. The agent may repeat itself; you review the result.
4. **Memory across sessions:** decisions land in the repo and in memory — not in the chat history.

> Start with one boring, important task. Not with the experiment "an agent replaces me".

<!-- notes:
(2 min) The transfer slide: the audience should be able to do one
thing tomorrow. Point 1 costs 20 minutes and changes everything —
the agent reads the contract on every start. Point 4: experiences /
spec repo instead of chat history.
-->

---

## Resources

- **openEduSuite** — `openedusuite.graphwiz.ai` · portal: `openedu.graphwiz.ai`
- **Workshop repo** (IT4Science Days 2026, 3h deck + exercises) — GitHub/Codeberg: `IT4Science-Days-2026-agentic-ai-workshop`
- **Tools:** pi (terminal agent) · OpenSpec (spec workflow) · taskfleet (agent fleet) · ArgoCD (GitOps)

Everything is tangible: repos, specs, test suites — no slide magic.

<!-- notes:
(30 s) Do not read aloud. Note: the workshop deck (3h version) is
public — anyone who wants to go deeper can do the exercises
themselves.
-->

---

<!-- _class: lead -->

# Thank you!

## Questions? — 10 minutes

Tobias Weiß · `tobias.weiss@uni-marburg.de`

GöAID · openEduSuite · University of Marburg

<!-- notes:
(10 min) Q&A. Likely questions: agent permissions/security (→
contract + plan mode + tests), model choice (→ harness is
model-agnostic, pi runs with various providers), cost (→ tight specs,
small orders), getting started (→ AGENTS.md + one boring task).
-->

# Agentic AI in Practice — From Spec to Productive Workflow

**Tobias Weiß · DevOps, University of Marburg · GöAID Session · 30 min + 10 min Q&A**

Agentic AI earns its keep in operations, not in demos. openEduSuite is a sovereign groupware suite on bare-metal Kubernetes. Its deployment, debugging and testing are done with AI agents under human contracts.

The method is a pyramid:

- **Spec** — scope and acceptance criteria
- **Contract** — the agent's rules, in the repo
- **Test** — CI decides when it is done

Four real cases from production:

1. Domain migration via a guarded, idempotent bootstrap script
2. SSO white page debugged to its root causes
3. Forgotten k8s directories dragged back under GitOps
4. A 59-check SSO test suite built by an agent fleet

Tools: pi (agent harness), OpenSpec (spec-driven changes), agentflow (parallel workers), pi-sandbox (key safety).

Attendees leave with a checklist: contract first, spec before code, CI as acceptance. Trust is good — verification is cheaper.

---

**TL;DR for the announcement:** How AI agents build, debug and operate a sovereign groupware suite on bare-metal Kubernetes — four real cases, one method: spec, contract, test.

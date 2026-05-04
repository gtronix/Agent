# Agentic workflow (general)

A practical pattern for using **goal-directed AI agents** beyond any single domain—software development, customer service, operations, and everyday knowledge work. It mirrors the same structural ideas as a disciplined offensive-security workflow: **intent**, **tools**, **guardrails**, and **feedback loops**.

---

## What counts as an agent

An **AI agent** is software that pursues specific goals by perceiving context, reasoning, planning, and acting through **tools** (APIs, browsers, terminals, ticket systems, calendars, etc.), often with light human oversight.

Compared with reactive chat or single-shot prompts, an agent is **proactive**: it can decide intermediate steps.

**Useful anchors:** goals, reasoning, memory (or persistent notes), tools.

> The agentic paradigm only works if you replace lost micromanagement with **operational discipline**.

---

## How this differs from “just prompting”

The model is mainly an **inference engine**: it decides *what to say or try next*.

- **What changes:** speed of iteration and breadth of tactics you can attempt.
- **What stays the same:** your underlying process (how you define done, quality, risk, and accountability).

**Typical loop**

1. **Inputs** — goal, scope, constraints, exclusions, special rules.
2. **Tools** — whatever the agent is allowed to call (IDE, DB read-only, CRM, email draft-only, etc.).
3. **Inference** — interpret, plan, reason, execute tool steps.
4. **Outputs** — tool results become the **next** inputs until the goal is met or blocked.

Inference alone drifts. **Context + inference + tools** produces something you can verify against reality.

---

## Operational discipline (levers you actually control)

| Lever | Purpose | Examples by domain |
|--------|---------|---------------------|
| **Guardrails** | Block or confirm before irreversible or sensitive actions | Dev: no prod deploy without approval. Support: no “account closed” without human. Personal: no send-email without draft review. |
| **Model choice** | Match cost, latency, privacy, reasoning depth | Fast model for triage; stronger model for architecture or escalations; local/offline for confidential code or PII-heavy tasks. |
| **Instruction files** | Stable context: project norms, tone, definitions, “definition of done” | `AGENTS.md`, support macros playbook, household rules for a personal assistant setup. |
| **Skills / playbooks** | Reusable procedures for recurring task classes | Code-review checklist; refund policy workflow; weekly finance reconciliation steps. |
| **Sub-agents or roles** | Split context and privilege | Research-only agent vs execution agent; L1 triage bot vs specialist escalation. |
| **Human involvement** | Choose semi-autonomous vs autonomous per risk | Autonomous for low-risk drafts; human-in-the-loop for money, legal, safety, reputation. |

---

## Front-load understanding (“pre-engagement”)

Before heavy execution, invest in clarity—same idea as reconnaissance, but generalized:

| Activity | Dev | Customer / ops | Personal / admin |
|----------|-----|------------------|------------------|
| **Map the landscape** | Repo tour, architecture notes, dependency overview | Product areas, known pain points, SLA | Accounts, recurring bills, calendars, key contacts |
| **Prioritize scenarios** | Riskiest paths, user journeys, failure modes | Top contact drivers, escalation triggers | Highest-impact chores or decisions this week |
| **Capture conversations** | Meeting notes → decisions and tickets | Call/chat summaries → CRM fields | Voice memo → structured tasks |
| **Research mode** | Issue reproduction, doc sweep, comparable implementations | Policy lookup, KB synthesis | Comparison shopping, travel constraints |

Non-agentic assistants (single-shot chats, templates) still save time here—use the right tier for the job.

---

## Task shape, planning, and delegation

These ideas apply to **any** goal-directed agent (coding, research, ops, personal workflows)—not only “research” roles. They mirror a disciplined lead/planner split: **understand → classify work shape → plan → execute with clear boundaries → synthesize → stop when good enough.**

### Assessment before execution

Before spending tokens or tool calls at scale, clarify:

- **Concepts and entities** — what the task is really about; dependencies between pieces.
- **Facts or artifacts needed** — what must be true or produced for “done.”
- **Constraints** — time, policy, tools allowed, audience, format.
- **Success shape** — report vs checklist vs code vs ticket fields; what the user likely cares about most.
- **Verification** — how you will know the output is correct (tests, sources, human review).

### Three work shapes (pick one primary)

| Shape | When it fits | Execution bias |
|--------|----------------|------------------|
| **Depth-first** | One core question, many valid angles (architecture tradeoffs, root-cause hypotheses, multi-stakeholder “why”). | Explore several **perspectives or methods** in parallel or sequence, then **synthesize** one coherent answer. |
| **Breadth-first** | Distinct sub-problems with weak coupling (multi-region rollout, compare three vendors, “fix these five unrelated bugs”). | **Partition** with crisp boundaries; run **parallel tracks**; aggregate into one deliverable. |
| **Straightforward** | Narrow, well-bounded task with an obvious path (single API check, one-file fix with tests). | **Shortest path**; minimal fan-out; explicit verification. |

Avoid splitting work that does not benefit from parallelism—**overhead** (coordination, duplicated context) can exceed gains.

### Plan quality checks

For each planned step, ask:

- Can this be broken into **independent** subtasks without harmful overlap?
- Would **multiple perspectives** reduce risk (unknown unknowns, adversarial review)?
- What is the **expected output** of this step (artifact shape, pass/fail)?
- Is this step **strictly necessary** for the stated goal?

### Lead vs workers (roles, not job titles)

- **Workers** (sub-agents, scripts, humans, or focused tool runs) handle **scoped gathering or execution**: read files, run tests, search docs, draft a slice of work.
- **Lead** (the coordinating thread) owns **plan updates, conflict resolution, and final synthesis**—the artifact that must read as one voice and one set of decisions.

Delegate substantial investigation or parallel exploration; **do not** delegate the final integrative judgment when accountability stays with the lead—mirror “don’t subcontract the executive summary to someone who didn’t see the whole picture.”

### Parallelism and fan-out

- Run **independent** operations together when your runtime supports it (multiple tools, multiple agents, CI jobs).
- Prefer **fewer, clearer scopes** over many tiny tasks—each split adds handoff cost.
- Order work by **dependency**: unblockers first; dependent steps after.

### Adaptation and stopping

- **Update the plan** when new facts arrive; treat earlier assumptions as revisable.
- When sources or tools **disagree**, weigh recency, independence of evidence, and consistency with other known facts—document residual uncertainty when stakes are high.
- When additional work has **diminishing returns** (good-enough answer within constraints), **stop** expanding scope—ship the draft, log gaps for a follow-up.

### Safety and sensitive topics

Do not spin off work whose purpose is abuse, harassment, or illegal activity. For legitimately sensitive domains (safety, healthcare, legal), **narrow scope** and **explicit constraints** in prompts to reduce harm; escalate to humans when policy or risk is unclear.

---

## Delivery: drafts vs ownership

Agents accelerate **first drafts** and **consistency** (code, emails, tickets, specs, slide outlines).

**Often improves**

- Time to first draft; parallel variants (A/B phrasing).
- Style consistency across docs or replies.
- Translation or localization with a human gloss pass.

**Still yours**

- Accountability for the final artifact.
- Fact-checking and hallucination control (claim-by-claim for high stakes).
- Severity or priority calibration (what is urgent vs noisy).
- Tone and trust (brand voice, empathy, political sensitivity).

---

## Feedback and documentation

Treat documentation as **fuel**, not wallpaper.

- Runbooks, decision logs, and “what went wrong” notes become **inputs** that improve the next run.
- Skills and templates should **accumulate** each cycle you complete deliberately.
- Guardrails and prompts should **evolve** from reviewed failures, not ad hoc hotfixes.

**What shifts:** the habit of capturing lightweight structure.  
**What stays:** judgment about what is worth codifying.

---

## Success criteria for the workflow

| Criterion | What “good” looks like |
|-----------|-------------------------|
| **Repeatability** | Environments and instructions reproducible; less “works on my machine” or “works on Tuesday.” |
| **Coverage** | Instructions explicit enough for breadth and depth you care about (tests, edge cases, unhappy paths). |
| **Self-improvement** | After each run: what failed, what to change in prompts, tools, or docs. |
| **Permissions / compliance** | Terms of service, data handling, industry rules; least privilege for tools. |
| **Documentation** | Outputs land where stakeholders expect (ticket fields, repo, wiki, CRM). |
| **Isolation / safety** | Sandboxes, staging, draft-only integrations—especially for destructive or external-facing tools. |
| **Efficiency** | Fewer wasted tokens and retries; dependencies and prerequisites declared up front. |
| **Control** | Human checkpoints where stakes warrant—semi-autonomous by default for risky domains. |

---

## Mapping needs to tooling (illustrative)

| Need | Typical building blocks |
|------|-------------------------|
| Isolated execution | Containers, scratch tenants, staging apps, separate support inbox |
| Repeatability | IaC, pinned deps, CI/CD, shared devcontainer or workspace templates |
| Coverage | Lint/test gates, review checklists, explicit acceptance criteria in instructions |
| Self-improvement | Issue templates, retros, changelog for prompts/skills |
| Efficiency | “Inventory” docs listing APIs, folders, credentials vault layout (not secrets themselves) |
| Visibility | Dashboards or logs so humans see what the agent did |

Approval-heavy vendors (e.g. regulated AI programs) sit beside **policy**—same workflow, stricter gates.

---

## Common failure modes

| Mode | Symptom | Mitigation |
|------|---------|------------|
| **Ambiguity** | Agent picks a plausible but wrong interpretation | Narrow prompts; examples; explicit definitions; ask clarifying questions in-policy |
| **Contradictions** | Mixed instructions across files or skills | Single owner for playbook merges; version skills; diff reviews like code |
| **Too much / too little context** | Noise drowns signal, or key facts missing | Tier context (summary + pointers); retrieve on demand; structured intake forms |
| **Hallucination** | Confident wrong facts | Ground with tools; cite sources; verify externally before irreversible steps |
| **Rushing** | Skipped validation | Treat agent output like a junior teammate’s PR: review; use version control |

---

## Semi-autonomous vs autonomous

- **Semi-autonomous:** narrow tasks with clear stop conditions—good when prerequisites matter (e.g. install the wordlist *before* brute force; reproduce the bug *before* refactor).
- **Autonomous:** broader goals with delegation—good when exploration is cheap and rollback is safe (e.g. organize notes into a outline; propose a test plan across modules).

Pick autonomy based on **blast radius**, not on hype.

---

## Minimal starter checklist

1. Write a one-page **instruction file**: goals, non-goals, tone, tools allowed, forbidden actions.  
2. Attach **2–3 skills** for your most repeated workflows.  
3. Add **guardrails** matching real risks (money, data, external comms, prod).  
4. Run one task **end-to-end**, then improve docs from what broke.  

---

## Mapping to the Agent template repository

This repo implements the pattern above with concrete files:

| Idea in this doc | Where it lives in the template |
|------------------|----------------------------------|
| Instruction files, definition of done | `AGENTS.md`, `app_spec.md`, `context/init.md`, `context/agent.md` |
| Task shape, planning, delegation | This doc (**Task shape, planning, and delegation**); specialized research-oriented wording in `docs/research_lead_agent.md` |
| Skills / playbooks | `skills/` (optional; copy into Cursor skills) |
| Guardrails | `AGENTS.md` defaults + explicit constraints in `app_spec.md` |
| Persistent notes / handoff | `context/session_history.md`, `context/feature_list.json` |
| Self-improvement after a run | Session log + optional `self-optimization` skill template |

Start from `README.md` and `AGENTS.md`.

---

*Companion to domain-specific playbooks (e.g. security assessments); this document stays intentionally general.*

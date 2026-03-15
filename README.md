# Principle-Driven Agentic Development (PDAD)

> Stop treating agentic development like it's just faster coding. It's a new discipline. PDAD is the framework for it.

---

## The Shift

Something is happening that most people are still processing.

Writing code stopped being the bottleneck. AI agents can ship features in hours that used to take sprints. The job of a software team is being rewritten in real time — and the rewrite isn't about code at all. It's about product thinking.

Everyone building with AI has become a product manager. Every time you prompt an agent, you're doing product management. The question isn't whether you're doing it — you are. The question is whether you're doing it well.

Most aren't. Because nobody handed them a framework.

The humans who thrive in this era won't be the best coders. They'll be the best at clarity: clear goals, clear principles, clear limits. PDAD is the operating system for that clarity.

---

## The Problem with Tickets

Agile, Scrum, tickets, roadmaps — these were designed to coordinate *humans* working on *code*. They solved the problem of "how do we get 10 developers to build the same thing?"

That problem is solved. Differently.

When an AI agent can implement your entire backlog in a weekend, the bottleneck isn't execution. It's **context**. The agent doesn't know what you're building, who it's for, why it matters, or where the edges are. So it guesses. It drifts. It over-engineers. It builds the wrong thing, beautifully.

Ticket queues don't fix this. You can write 50 Jira tickets and still give an agent zero context about product direction.

The new bottleneck is: what you put in front of the agent before it starts.

---

## The Context Stack

Five documents. That's PDAD.

These aren't a product spec or a PRD. They're the persistent context layer that lives above any individual task — the thing you write once and refine forever, giving every agent run a foundation to build on.

```
Goals → North Star → Principles → Guardrails → Anti-Goals → Outcome Spec
```

### Goals

**What you're building, for who, and what success looks like.**

Three components, all required:

**Audience (ICP)** — Specific, not generic. Not "musicians." Not "developers." The tighter this is, the better the output.

> *Bad:* "Indie musicians"
> *Good:* "Indie artists with 500–5k monthly Bandcamp listeners who've never run a paid promo and don't have a marketing budget"

**User Outcome (JTBD)** — What the user achieves. Framed as a job to be done.

> *Bad:* "Users can see their analytics"
> *Good:* "Artist books 3x more streams in 30 days without needing to understand marketing or spend time on it"

**Business Outcome** — What the business needs. Metric-driven, time-bound.

> *Bad:* "Grow revenue"
> *Good:* "20% of trial users convert to paid within 14 days of signup"

---

### North Star

**The single metric the product is optimizing for right now.**

Goals define success broadly. The North Star narrows it to one number. If you could only move one metric this quarter, what is it? That's your North Star.

It's not revenue. Revenue is the output. The North Star is the leading indicator — the thing that, when it moves, everything else follows.

> *Bad:* "Grow the platform"
> *Good:* "Crates created by non-admin users per week"

Notice what that example excludes: admin activity, operator setup, seeded content. Only real user behavior counts. If you're the one creating all the crates, the metric is lying to you.

One North Star per product at a time. When strategy shifts, update it. But don't run two — that's not focus, that's hedging.

The North Star drives Research. Every cycle, you audit the funnel that produces it (see Funnel Audit below). You can't improve what you're not measuring.

---

### Principles

**How you build. The quality standard baked into every decision.**

Principles answer: *When there's a tradeoff, what do we prioritize?*

Example:
- Ship working code over perfect code; iterate in production
- Every feature must be measurable before it ships
- Prefer reversible decisions; flag irreversible ones for human review
- No feature without a tracking event
- Optimize for the first-time user, not the power user
- Fail loudly — errors should surface, not be swallowed

5–10 is the right range. More than that and nothing is actually a principle. Write them as active statements, not corporate values. Test them: if an agent followed every principle, would you be happy with what it built?

---

### Guardrails

**What must NEVER happen. Hard limits. Non-negotiable.**

Guardrails exist because agents, without constraints, will do things that seem logical in isolation but are catastrophic in context.

Example:
- Never break existing user flows without a deprecation path
- Never send external communications without human approval
- Never touch billing or authentication systems autonomously
- Never deploy without all tests passing
- Never delete production data without a backup confirmed

Guardrails serve double duty: they're not just constraints — they're **the oversight mechanism baked into context**. When an agent hits a Guardrail, it stops and surfaces a decision. You don't need to watch every commit. You need to write good constraints upfront.

**Guardrails vs. Principles:**
- Principles = how to do things right
- Guardrails = what never to do, full stop

---

### Anti-Goals

**What you are explicitly NOT building. Strategic decisions, not safety ones.**

Anti-goals prevent two common failure modes:
1. **Agent drift** — agent builds more than asked, in a direction that doesn't fit
2. **Over-engineering** — agent gold-plates features you don't need

Example:
- We are not building a social network or community features
- We are not optimizing for power users at the expense of first-timers
- We are not trying to compete with Spotify or major DSPs
- We are not building a mobile app (yet)

**Anti-goals vs. Guardrails:**
- Guardrails = safety/compliance (never do X, period)
- Anti-goals = strategy (we're not going in that direction, for business reasons)

Update anti-goals as strategy changes. Yesterday's anti-goal may be tomorrow's roadmap.

---

### Outcome Spec

**The specific deliverable for this agent session. Changes every run.**

This is the bridge between persistent product context and the agent's actual task.

Components:
- **Deliverable** — What, specifically, is being built
- **Scope In** — What's explicitly included
- **Scope Out** — What's explicitly excluded
- **JTBD Frame** — Who's doing what job, and why it matters
- **Done looks like** — How you'll know it's complete

Example:
```
Deliverable: Email onboarding sequence (3 emails)
Scope In: Welcome email, feature discovery email, upgrade prompt
Scope Out: Transactional emails, marketing campaigns, A/B testing
JTBD: New trial user understands core value and knows what to do next
Done: Emails send in staging, copy reviewed, tracking events firing
```

---

## Autonomy Tiers

Not all tasks are equal. Different work requires different levels of human oversight. PDAD uses four tiers to define how much autonomy an agent has for a given task.

| Tier | Name | Description | Examples |
|------|------|-------------|---------|
| **T1** | Full Autonomy | Agent executes, commits, and deploys without check-in | Bug fixes, copy edits, test additions, dependency updates |
| **T2** | Propose + Execute | Agent proposes approach, gets approval, then executes | New features, schema changes, refactors |
| **T3** | Propose Only | Agent researches and proposes; human executes or explicitly delegates | Architecture decisions, major UX changes, new integrations |
| **T4** | Human Only | Agent assists but human makes the call and does the work | Billing changes, auth systems, external communications, deletions |

**Assign tiers at the task level, not the project level.** A single agent run might have T1 work (fix this typo) and T4 work (update the pricing page). Name both explicitly.

See [AUTONOMY-TIERS.md](AUTONOMY-TIERS.md) for the full decision framework.

---

## Work Item Design

**Work items in PDAD are not tickets. Three fields make them different.**

A Jira ticket says: *"Build X."* A PDAD work item says: *"We believe building X will cause Y, because Z."* That difference matters more than any methodology.

**Hypothesis** — "We believe X will improve Y because Z." Every work item is a bet. If you can't write the hypothesis, you don't understand why you're building it. No hypothesis, no work item. This isn't bureaucracy — it's a forcing function for clarity.

> *Bad:* "Add email notifications"
> *Good:* "We believe adding email notifications when a crate gets a new follower will increase weekly return visits by 15%, because users currently have no signal that their crates are gaining traction."

**Acceptance Criteria** — Defined before building starts, not after. This is where most teams cheat: they write the criteria after delivery to confirm what was already built. That's theater. Real acceptance criteria are written as pass/fail conditions before a line of code is written. If you can't say in advance what "done" looks like, you're not ready to build.

**ICE Score** — Impact × Confidence × Ease (each 1–3, max 27). Forces prioritization before the queue forms. Highest-ICE items ship first. The score isn't precise — it's directional. The point is to have a conversation about the tradeoffs before you're committed.

This connects to the Latent Space "code review is dead" insight: human judgment moves upstream. When agents do the building, you're not reviewing the diff — you're reviewing the spec. The hypothesis, the acceptance criteria, the ICE score. Get those right and the execution largely takes care of itself.

---

## Active Tests

**Shipping isn't the end of the loop — it's the beginning of measurement.**

Every work item with a hypothesis auto-creates an Active Test on deploy. Active Tests are persistent monitoring items, not tasks. They don't close when the feature ships. They close when the hypothesis is confirmed, refuted, or declared inconclusive.

An Active Test tracks:
- **What's being tested** — the feature or change
- **Hypothesis** — copied from the work item
- **Success metric** — the specific number that determines the outcome
- **Current reading** — latest data
- **Status** — running / concluded / inconclusive

The research process checks all running Active Tests on every cycle. A test that's been running for more than 4 weeks without a conclusion is itself a signal — either the metric isn't being captured, or the effect is too small to measure, or nobody's actually looking. All three are problems.

Concluded tests feed back into your PDAD documents. A confirmed hypothesis might strengthen a Principle. A refuted one might become an Anti-Goal. An inconclusive one probably means you're missing instrumentation.

You can't learn from what you didn't measure.

---

## The Oversight Layer

This is the part nobody in the "vibe coding" discourse is talking about.

Everyone's focused on unlocking AI. Almost nobody is asking: *How do you know what the agent is actually building?* When do you intervene vs. let it run? How do you maintain product coherence across 50 agent runs?

The answer isn't better logging or dashboards (though those help). The answer is **constraints baked into context before the agent starts**.

Guardrails and Anti-goals aren't just product documents — they're your oversight mechanism. An agent that knows it must never touch billing autonomously will surface billing-adjacent work for human review, automatically. An agent that knows you're not building a social network won't go there, even when a feature "naturally" leads that direction.

You don't need to watch every commit. You need to write good constraints upfront.

That's observability you can actually maintain.

---

## PDAD + Spec Kit

PDAD is the product layer. Spec Kit is the task layer. They're designed to work together.

| Layer | Tool | Question Answered | Lifecycle |
|-------|------|-------------------|-----------|
| **Product** | PDAD | What are we building, for who, and why? | Persistent — updated, never replaced |
| **Task** | Spec Kit | How does this specific piece get done? | Per-session — created and closed |
| **Execution** | Agent | Does the work | Stateless — consumes both layers |

**Spec Kit without PDAD** gives you perfectly executed wrong things.

**PDAD without Spec Kit** gives you well-intentioned vague instructions.

**Both together** give agents what they need to build the right thing, right.

When starting an agent session, combine them:

```markdown
## Product Context (PDAD)

**Goals:**
- Audience: [ICP definition]
- User Outcome: [JTBD statement]  
- Business Outcome: [metric + timeframe]

**North Star:** [single metric the product is optimizing for right now]

**Principles:** [5-8 active statements]

**Guardrails:** [hard limits as "Never X"]

**Anti-goals:** [what you are NOT building]

## Task Context (Outcome Spec)

**Deliverable:** [specific output]
**In scope:** [explicit inclusions]
**Out of scope:** [explicit exclusions]
**Done looks like:** [completion criteria]
```

---

## The Loop

PDAD isn't a one-time setup. It's a living system that improves with every agent run.

```
Research (funnel audit + active test check) →
Propose (with hypothesis + acceptance criteria + ICE score) →
Approve →
Build →
Deploy →
Monitor (auto-test created from hypothesis) →
Learn (research checks tests, closes loop)
```

1. **Research** — Agent explores the codebase, surfaces options, identifies risks. When a North Star exists, this step includes a **Funnel Audit**: map every stage that produces the North Star metric (typically Acquisition → Conversion → Activation → Retention), then ask two questions for each stage: *Do we have visibility?* and *Is there a work item targeting it?* Missing instrumentation is a blocker, not a nice-to-have. You can't optimize what you can't measure. Research also checks all running Active Tests — any test due for a conclusion gets surfaced.

2. **Propose** — Agent writes a work item: deliverable, hypothesis, acceptance criteria, ICE score. Human reviews before execution starts. This is where judgment happens — not at the diff.

3. **Approve** — Human signs off (or adjusts) the plan. The hypothesis must make sense. The acceptance criteria must be unambiguous. The ICE score must reflect actual tradeoffs.

4. **Build** — Agent executes with full PDAD context loaded.

5. **Deploy** — Ship it.

6. **Monitor** — An Active Test is automatically created from the work item's hypothesis. It starts running from deploy. The success metric is tracked.

7. **Learn** — Next Research cycle checks all running Active Tests. Concluded tests update PDAD documents. Every drift, every surprise, every "I didn't want it to do that" is a missing Guardrail or Anti-goal. Capture it.

The Learn step is what most people skip. Don't skip it. Over time, your PDAD documents become a high-fidelity model of how you build. The agents get better not because they improved — because you got better at giving them context.

---

## Related Ideas

**Zombie SaaS Revival** is PDAD's most interesting use case.

The premise: acquire zombie SaaS products at distressed valuations — products with 50–500 paying customers, flat MRR, no active dev. Most aren't dead because the idea was bad. They're dead because the founder ran out of energy. AI doesn't run out of energy.

With PDAD as the operating system, you can run a portfolio of dead products with a single operator: one PDAD stack per product, AI agents handling support, shipping features, running marketing. The "who's going to do all the work?" problem disappears.

The bottleneck was never the idea. It was the humans.

More in [zombie-saas-idea.md](zombie-saas-idea.md) (coming soon).

---

## Status

This is a living document. PDAD is being built and tested in production at [GetMusic.fm](https://getmusic.fm), [IndieCrates](https://indiecrates.com), [SonicSift](https://sonicsift.com), and [Glance](https://glnc.io).

If you're using PDAD, open an issue and tell us what's working and what's not.

---

## License

MIT — see [LICENSE](LICENSE)

---

## PDAD v3 — Work Queue & Deploy System

The context stack above is the *product* layer. PDAD v3 adds an opinionated *execution* layer: version-controlled work queues, category-based auto-approvals, and explicit deploy gates.

### How it works

Each project gets a `pdad/` directory:
- `README.md` — what this product is, north star metric
- `work-queue.md` — approved items ready to build or deploy
- `ideas.md` — raw backlog, not yet reviewed
- `decisions.md` — why we built or skipped things
- `principles.md` — product rules and hard constraints

See [`SPEC.md`](SPEC.md) for the full v3 specification (categories, status flow, quality gates, deploy flow).  
See [`templates/`](templates/) for blank starting files.

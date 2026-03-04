# Autonomy Tiers — Decision Framework

Not all agent tasks are equal. Running a linter is different from changing your pricing page. PDAD uses four autonomy tiers to define how much a human needs to be in the loop for any given task.

The tiers aren't about trust in the AI. They're about the **reversibility and blast radius** of the action.

---

## The Four Tiers

### Tier 1 — Full Autonomy

**Agent executes, commits, and deploys without check-in.**

Use when:
- The action is easily reversible (can be undone with a revert)
- The blast radius is small (affects one component, one file, one feature)
- The task is well-understood and unambiguous
- Failure is caught by tests or monitoring before it reaches users

Examples:
- Bug fixes with clear reproduction steps
- Copy edits and typo corrections
- Adding or updating tests
- Dependency version bumps (with tests passing)
- Code style / lint fixes
- Documentation updates
- Internal tooling changes

What "full autonomy" means in practice:
- Agent executes without proposing first
- Commits directly to working branch
- Deploys to production if tests pass
- Reports back when done

---

### Tier 2 — Propose + Execute

**Agent proposes approach, gets human approval, then executes.**

Use when:
- The change is significant but the scope is bounded
- There's more than one reasonable approach and the choice matters
- The work touches multiple components or files
- A mistake would require meaningful effort to reverse

Examples:
- New features (non-trivial)
- Database schema changes
- Refactors that affect multiple files
- New third-party integrations
- Changes to user-facing workflows
- Performance optimizations with tradeoffs

What "propose + execute" looks like:
1. Agent researches and writes a short proposal (approach, tradeoffs, what it will and won't touch)
2. Human reviews and approves (or asks for changes)
3. Agent executes with full context, commits, and reports back
4. Human reviews output before deploying (or delegates that to the agent)

The proposal should be short — a few sentences or a bullet list, not a document. The goal is to surface the key decision before work starts, not to create process theater.

---

### Tier 3 — Propose Only

**Agent researches and proposes; human executes or explicitly delegates.**

Use when:
- The decision has long-term consequences that are hard to reverse
- The change sets a direction that constrains future work
- Multiple stakeholders need to be aware or aligned
- You want full human judgment before any code is written

Examples:
- Architecture decisions (new services, data models, infrastructure)
- Major UX changes that affect the core user journey
- New external integrations that involve contracts or compliance
- Deprecating or removing significant features
- Pricing or packaging changes
- Changes to onboarding or activation flows

What "propose only" looks like:
1. Agent researches the problem thoroughly
2. Agent writes a clear proposal with options, tradeoffs, and a recommendation
3. Human reviews, decides, and either executes or hands back to agent with explicit authorization to proceed
4. If handed back, becomes a T2 task with the decision already made

The key: human makes the call. Agent provides the research and the recommendation, not the implementation.

---

### Tier 4 — Human Only

**Agent assists but human makes the call and does the work.**

Use when:
- The action cannot be undone or is extremely difficult to reverse
- The blast radius is company-wide or customer-facing in a high-stakes way
- Legal, financial, or compliance implications
- External parties are involved

Examples:
- Billing and subscription system changes
- Authentication and access control modifications
- External communications (emails, announcements, support responses)
- Production database deletions or migrations with no rollback
- Security-sensitive code (encryption, key management)
- Any action that affects all users simultaneously

What "human only" looks like:
- Agent can research, draft, and assist
- Agent surfaces the work and explains what needs to happen
- Human makes the decision and takes the action
- Agent does not execute autonomously, even with explicit instruction in the moment

T4 is also where your Guardrails live. If a Guardrail covers an action, it's T4 by definition.

---

## Decision Framework

When assigning a tier to a task, ask these questions in order:

### 1. Is this covered by a Guardrail?
**Yes →** T4. No exceptions. Guardrails exist precisely for this.

### 2. Is this easily reversible?
**Yes + small blast radius →** T1
**Yes + larger blast radius →** T2

### 3. Does this set a direction that constrains future work?
**Yes →** T3 or T4 depending on reversibility

### 4. Does this affect billing, auth, or external communications?
**Yes →** T4

### 5. Is the approach unambiguous?
**Yes + small scope →** T1
**Yes + larger scope →** T2
**No →** T3 (agent needs to propose options first)

---

## Quick Reference

```
Easily reversible + small scope          → T1 (just do it)
Significant but bounded + reversible     → T2 (propose first)
Sets long-term direction                 → T3 (human decides)
Guardrail-covered or irreversible        → T4 (human executes)
```

---

## Assigning Tiers in Practice

**Assign tiers at the task level, not the project level.**

A single agent session might include:
- Fix this broken test → T1 (just fix it)
- Add email notifications to the onboarding flow → T2 (propose approach first)
- Decide between Postgres full-text search or Elasticsearch → T3 (research and recommend)
- Update the Stripe webhook handler for the new pricing → T4 (human does this)

Name the tier explicitly in your Outcome Spec. The agent needs to know which parts it can execute freely and which parts require a pause.

**Example Outcome Spec with tiers:**

```
Deliverable: Improve search performance

Tasks:
- Add database indexes for common query patterns (T1 — just do it, tests will catch regressions)
- Refactor search controller to reduce N+1 queries (T2 — propose approach before touching)
- Evaluate Elasticsearch vs. Postgres full-text for long term (T3 — research and recommend, I'll decide)
```

---

## When in Doubt

Default to the more conservative tier. A T2 that could have been T1 costs you one approval cycle. A T1 that should have been T2 can cost you a production incident.

The tiers exist to make the implicit explicit. Every agent task has a natural tier — PDAD just makes you name it upfront.

---

*AUTONOMY-TIERS.md — part of [Principle-Driven Agentic Development](https://github.com/chuckblake/Principle-Driven-Agentic-Development)*

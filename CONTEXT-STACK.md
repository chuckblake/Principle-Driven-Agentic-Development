# The Context Stack — Project Template

Use this template to create PDAD context for your own project. Fill in each section, delete the instructions, and give it to your agent at the start of every session.

**How to use this:**
1. Copy this file into your project as `PDAD.md`
2. Fill in all five documents for your product
3. Keep it in version control — it's a living document
4. Update it after every significant agent run

---

## Document 1: Goals

> *Define what you're building, for who, and what success looks like. All three components are required. Be specific — vague goals produce vague output.*

### Audience (ICP)

Who is this product for? Be ruthlessly specific. Think about: who they are, what they do, their skill level, their context, where they are in their journey, their volume/stage.

```
[Your ICP here]

Example: "Indie artists with 500–5k monthly Bandcamp listeners who've never run 
a paid promo and don't have a marketing budget"

NOT: "Musicians" or "Developers" or "Small businesses"
```

### User Outcome (JTBD)

What does the user achieve? Frame it as a job to be done — something they're trying to accomplish in their life, not a feature list.

```
[Your user outcome here]

Example: "Artist books 3x more streams in 30 days without needing to understand 
marketing or spend time on it"

NOT: "Users can see their analytics" or "Users get access to X feature"
```

### Business Outcome

What does the business need? Metric-driven, time-bound where possible.

```
[Your business outcome here]

Example: "20% of trial users convert to paid within 14 days of signup"

NOT: "Grow revenue" or "Get more users"
```

---

## Document 2: Principles

> *How you build. Your quality standard. The philosophy baked into every decision. Write as active statements. 5–10 is the right range — more than that and nothing is actually a principle.*

```
1. [Principle]
2. [Principle]
3. [Principle]
4. [Principle]
5. [Principle]

Suggested starting points (keep, modify, or replace):
- Ship working code over perfect code; iterate in production
- Every feature must be measurable before it ships
- Prefer reversible decisions; flag irreversible ones for human review
- No feature without a tracking event
- Optimize for the first-time user, not the power user
- Fail loudly — errors should surface, not be swallowed
- Style/lint passes before every commit
```

**Test your principles:** If an agent followed every principle to the letter, would you be happy with what it built?

---

## Document 3: Guardrails

> *What must NEVER happen. Hard limits. Non-negotiable. Write in negative form: "Never X." These should make you slightly uncomfortable — if they're easy, they're not real limits.*

```
- Never [hard limit]
- Never [hard limit]
- Never [hard limit]
- Never [hard limit]

Suggested starting points (keep, modify, or add):
- Never break existing user flows without a deprecation path
- Never send external communications without human approval
- Never touch billing or authentication systems autonomously
- Never deploy without all tests passing
- Never delete production data without a backup confirmed
- Never modify access control without explicit human sign-off
```

**A good Guardrail:** Violating it would be a serious problem. If it wouldn't matter much, it's not a Guardrail.

---

## Document 4: Anti-Goals

> *What you are explicitly NOT building. Strategic decisions, not safety ones. These prevent agent drift and over-engineering. Update them as strategy evolves.*

```
- We are not [strategic exclusion]
- We are not [strategic exclusion]
- We are not [strategic exclusion]

Examples:
- We are not building a social network or community features
- We are not optimizing for power users at the expense of first-timers
- We are not trying to compete with [major competitor]
- We are not building a mobile app (yet)
- We are not collecting more data than we need to provide core value
```

**Anti-goals vs. Guardrails:**
- Guardrails = safety/compliance (never do X, period)
- Anti-goals = strategy (we're not going in that direction, for business reasons)

---

## Document 5: Outcome Spec

> *The specific deliverable for THIS agent session. This document changes every run — Goals/Principles/Guardrails/Anti-goals are persistent; Outcome Spec is per-session.*

```
**Deliverable:** [What, specifically, is being built]

**Scope In:**
- [Explicit inclusion]
- [Explicit inclusion]

**Scope Out:**
- [Explicit exclusion]
- [Explicit exclusion]

**JTBD Frame:** [Who is doing what job, and why it matters now]

**Done looks like:**
- [Completion criterion]
- [Completion criterion]
- [Completion criterion]
```

---

## Putting It Together

When starting an agent session, provide context in this order:

```markdown
## Product Context (PDAD)

**Goals:**
- Audience: [your ICP]
- User Outcome: [your JTBD statement]
- Business Outcome: [your metric + timeframe]

**Principles:**
[your principles, one per line]

**Guardrails:**
[your hard limits, "Never X" format]

**Anti-goals:**
[your strategic exclusions, "We are not..." format]

## Task Context

**Deliverable:** [specific output for this session]
**In scope:** [explicit inclusions]
**Out of scope:** [explicit exclusions]
**Done looks like:** [completion criteria]
```

---

## Maintenance

**After every significant agent run, ask:**

1. Did the agent go somewhere unexpected? → Add an Anti-goal
2. Did it do something you'd never want repeated? → Add a Guardrail
3. Did the ICP shift based on what you learned? → Update Goals
4. Did the tradeoff it made feel wrong? → Update or add a Principle

PDAD gets sharper with use. The version you have after 50 agent runs is better than the version you started with — because it has the fingerprints of real decisions.

---

*PDAD Template — part of [Principle-Driven Agentic Development](https://github.com/chuckblake/Principle-Driven-Agentic-Development)*

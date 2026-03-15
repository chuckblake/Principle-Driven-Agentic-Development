# PDAD v3 — Full Specification

## Philosophy
- **No surprise deployments.** Builder builds and tests. Owner deploys.
- **Categories carry the rules.** The type of work determines what's auto-approved — no abstract tier numbers.
- **Everything lives in the repo.** PDAD context is version-controlled alongside the code it describes.
- **Quality gates are non-negotiable.** Tests pass or nothing ships.

## Work Categories & Auto-Approve Rules

| Category | Examples | Auto-Approved? |
|----------|----------|----------------|
| `bug-fix` | Broken feature, error 500, wrong output | ✅ Yes |
| `ux-polish` | Copy edits, spacing, loading states, small UI tweaks | ✅ Yes |
| `performance` | Query optimization, caching, N+1 fixes | ✅ Yes |
| `refactor` | Code cleanup, linting, test coverage (no behavior change) | ✅ Yes |
| `new-feature` | New user-facing functionality | ❌ Owner review |
| `schema-change` | Migrations, new columns, index changes | ❌ Owner review |
| `auth-security` | Auth flow, permissions, API keys | ❌ Owner review |
| `navigation-flow` | Route changes, page structure, onboarding flow | ❌ Owner review |
| `external-integration` | New APIs, webhooks, third-party services | ❌ Owner review |

> Auto-approved = builder can start work immediately. All items still require owner to trigger the deploy.

## Work Item Schema

```yaml
## PROJ-042 · Title here

category: bug-fix
status: approved
auto_approved: true
priority: high
created: 2026-03-14
deploy_trigger: manual

### Problem
What's broken or missing.

### Acceptance Criteria
- Specific, testable outcomes
- Tests must cover the change

### Notes
Any relevant context.
```

## Status Flow

```
idea → approved → in-progress → ready-to-deploy → deployed → archived
```

| Status | Meaning |
|--------|---------|
| `idea` | In ideas.md — not yet reviewed |
| `approved` | Greenlit — builder can pick it up |
| `in-progress` | Builder actively working |
| `ready-to-deploy` | Built, tested, PR merged — waiting for owner to deploy |
| `deployed` | Live in production, health check passed |
| `archived` | Skipped or superseded — decision logged in decisions.md |

## Quality Gates (Non-Negotiable)

### Gate 1 — Test Coverage
- All changed files must have test coverage
- Existing tests must pass (CI blocks merge)
- Tests written alongside code, not after
- No untested code ships. Ever.

### Gate 2 — Post-Deploy Health Check
1. Wait 90 seconds for server to spin up
2. Hit key endpoints and verify HTTP 200 responses
3. **If failure:** auto-rollback runs + owner alert sent
4. **If success:** confirmation sent to owner

## Deploy Flow

```
Builder builds → tests pass (CI green) → PR merged
       ↓
status: ready-to-deploy
       ↓
Owner briefing: "X items ready to deploy"
       ↓
Owner says "deploy it"
       ↓
Deploy runs → health check → ✅ confirm  or  ❌ auto-rollback + alert
```

Owner is always the deploy trigger. No auto-deploys. No 3am surprises.

## Builder Workflow
1. Check `work-queue.md` for `status: approved` items
2. Confirm category is auto-approved OR wait for owner OK
3. Update status to `in-progress`
4. Read `principles.md` before touching code
5. Build + write tests concurrently
6. Run linter
7. Open PR — CI must go green before merge
8. Merge PR → update status to `ready-to-deploy`
9. Report back: "PROJ-042 ready to deploy"

## Project Directory Structure

Each project using PDAD gets a `pdad/` directory:

```
pdad/
├── README.md       — what this product is, north star metric
├── work-queue.md   — approved items ready to build or deploy
├── ideas.md        — raw backlog, not yet reviewed
├── decisions.md    — why we built or skipped things
└── principles.md   — product rules and hard constraints
```

See `templates/` for blank starting files.

# PDAD — Product Development as a Document

A lightweight product development framework for indie devs. Version-controlled work queues, category-based auto-approvals, and deploy gates — all living in your repo alongside your code.

## How it works

Each project gets a `pdad/` directory:
- `README.md` — what this product is, north star metric
- `work-queue.md` — approved items ready to build or deploy
- `ideas.md` — raw backlog, not yet reviewed
- `decisions.md` — why we built or skipped things
- `principles.md` — product rules and hard constraints

See `SPEC.md` for the full framework spec.

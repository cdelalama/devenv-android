<!-- doc-version: 0.2.5 -->
# LLM Start Guide - devenv-android

## Read This First

Recommended order:
1. This file
2. `README.md`
3. `docs/PROJECT_CONTEXT.md`
4. `docs/VERSIONING_RULES.md`
5. `docs/llm/HANDOFF.md`
6. `docs/llm/DECISIONS.md`

## Critical Rules

### Language Policy

- Code, comments, and docs: English
- Conversation with the user: Spanish

### Documentation Rules

- Update `docs/llm/HANDOFF.md` when the repo state or focus changes
- Append a session entry to `docs/llm/HISTORY.md` whenever you do work here
- Put durable rationale in `docs/llm/DECISIONS.md`
- Keep this file's Current Focus aligned with `docs/llm/HANDOFF.md`

### Versioning Rules

- `VERSION` is the source of truth
- Use `scripts/bump-version.sh <new_version>` for version bumps
- Validate with `scripts/check-version-sync.sh`
- Any commit that changes product code/config should include a version bump

## Current Focus

Source of truth: `docs/llm/HANDOFF.md`.

- Last Updated: 2026-09-12 - GPT-5 Codex
- Working on: keep the Android client boundary explicit after the devenv-stack rebrand
- Status: v0.2.5 registers the repository for central DocKit discovery and adopts the independent-review policy; Android behavior remains unchanged

## Current Risk To Keep In Mind

The main risk in this repo is reintroducing a second non-Termux or non-`devenv`
workflow by accident.

## Checklist

- Read `README.md`
- Read `docs/PROJECT_CONTEXT.md`
- Read `docs/VERSIONING_RULES.md`
- Read `docs/llm/HANDOFF.md`
- Do the work
- Update `docs/llm/HANDOFF.md`
- Append to `docs/llm/HISTORY.md`
- If version changes, run `scripts/bump-version.sh`

## Quick Navigation

- Overview: `README.md`
- Project context: `docs/PROJECT_CONTEXT.md`
- Repo structure: `docs/STRUCTURE.md`
- Version rules: `docs/VERSIONING_RULES.md`
- Handoff: `docs/llm/HANDOFF.md`
- History: `docs/llm/HISTORY.md`
- Decisions: `docs/llm/DECISIONS.md`

---

Do not use this repo as a second source of workspace truth. It is a client layer.

<!-- DOCKIT-TEMPLATE:START independent-review-policy -->
### Independent Review Policy

For consequential source candidates that require an independent model review,
the operator-wide default is:

1. Prefer Fable, exact model `claude-fable-5-1`, with high effort.
2. If direct quota evidence shows that exact Fable is unavailable because its
   quota is exhausted, Opus may complete the same review gate using exact model
   `claude-opus-5[1m]`, with high effort. Record the quota evidence, effective
   model, effort, command, candidate revision/tree, and validation packet in
   `docs/llm/REVIEWS.md` when it exists, otherwise in the audited revision's
   HISTORY entry. When durable Trace is enabled, keep non-commit object IDs such
   as tree hashes as plain text in HISTORY and HANDOFF Trace Anchors:
   backtick-quoted hashes are reserved for commit provenance and must resolve as
   commits. Never remove backticks from a commit to bypass validation; classify
   a cross-repository commit with the Trace `external=repo@hash` field instead.
3. Never substitute Sonnet, Haiku, an ambiguous alias, or an unrecorded model.
   If neither allowed exact model is available, freeze the candidate and audit
   packet. Continue only work already authorized that does not depend on the
   missing verdict.

The auditor is independent and read-only: it reads primary files and evidence,
does not edit the candidate, and returns evidence-backed findings. The executor
must verify each finding, reconcile disagreements with the same auditor session
where practical, and preserve explicit unresolved disagreement for the
operator. A review verdict does not authorize build, deployment, runtime,
secrets, infrastructure, lifecycle, or acceptance changes.

This synchronized section is the fleet default, not permission to weaken an
existing project contract. A stricter project-local accepted rule wins until
the operator explicitly supersedes it. Projects that intentionally own a
different policy may exclude `independent-review-policy` in
`.dockit-config.yml`; the exception and rationale must remain visible locally.
<!-- DOCKIT-TEMPLATE:END independent-review-policy -->

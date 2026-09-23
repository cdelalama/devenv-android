<!-- doc-version: 0.2.6 -->
# LLM Start Guide - devenv-android

- Last Updated: 2026-09-23 - Codex (DocKit fleet update).
- Tooling update: see `docs/llm/DOCKIT_ADOPTION.md`; historical project status below is preserved.

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

The operator-wide Claude default is Opus 5.5, exact model
`claude-opus-5-5`, with high effort. This applies to Claude advisory/coauthor
work and independent source review unless the operator explicitly selects a
different model for the task. The operator's 2026-09-23 decision supersedes the
previous inherited Fable-first / quota-only Opus fallback preference.

1. Select the exact model explicitly for non-interactive review; do not use a
   floating `opus`, `best` or `default` alias as audit provenance.
2. Record effective model, effort, command, candidate revision/tree and validation
   packet in `docs/llm/REVIEWS.md` when present, otherwise the audited revision's
   HISTORY entry. Verify returned model metadata; a self-reported model name in
   the answer is not evidence. Do not silently substitute Fable, older Opus,
   Sonnet, Haiku or another model. If the selected model is unavailable or the
   provider changes it, preserve the packet and keep the required review gate
   open; continue only authorized work that does not depend on that verdict.
3. When durable Trace is enabled, keep non-commit object IDs such as tree hashes
   as plain text in HISTORY and HANDOFF Trace Anchors. Backtick-quoted hashes are
   reserved for commit provenance and must resolve as commits. Never remove
   backticks from a commit to bypass validation; classify a cross-repository
   commit with the Trace `external=repo@hash` field instead.

The auditor is independent and read-only: it reads primary files and evidence,
does not edit the candidate, and returns evidence-backed findings. The executor
must verify each finding, reconcile disagreements with the same auditor session
where practical, and preserve explicit unresolved disagreement for the operator.
A review verdict does not authorize build, deployment, runtime, secrets,
infrastructure, lifecycle or acceptance changes.

This synchronized section changes the model preference, not other project review
requirements. Explicit task-specific operator choices remain authoritative. A documented
operator-approved project model exception remains an exception until explicitly
superseded; exclusion alone is not approval of a different model. Other project
review constraints remain in force. Projects that exclude this section through
`.dockit-config.yml` must keep the exception and its authority visible.
The source policy belongs to LLM-DocKit; Claude Code's user `model` setting is a
separate runtime default and does not prove that project copies were synchronized.
<!-- DOCKIT-TEMPLATE:END independent-review-policy -->


<!-- DOCKIT-TEMPLATE:START delivery-evidence -->
## Optional Delivery Controls

For repeated delivery/infrastructure attempts, adopt `docs/DELIVERY_CONTRACT.md`
in the actual project mutation command. The project runs the real prerequisite
probe, records its observation, and calls `scripts/dockit-delivery-record.sh begin`
immediately before mutation; it records outcome and recovery afterward.

Copying scripts or a passing session validator is not integration. Require the
project's rerunnable negative test to demonstrate zero mutation calls for a failed
prerequisite, plus a current candidate-bound integration receipt. The journal
preserves attempt/review counts across sessions and versions. Repeating a failed
causal state or exhausting a budget requires bounded reassessment, never automatic
approval. Existing independent review and operational authority still apply.
Recovery must remain available independently of ordinary delivery checks.

Keep source publication, deployment and actual user acceptance separate. A short
HANDOFF names the observed result, current blocker and next concrete step.
<!-- DOCKIT-TEMPLATE:END delivery-evidence -->

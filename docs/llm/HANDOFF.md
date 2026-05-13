<!-- doc-version: 0.2.4 -->
# Handoff - devenv-android

## Current Status

- **Last updated**: 2026-05-13 - Claude Opus 4.7 (1M context)
- **Focus**: Fixed the post-rebrand config-path mismatch so runtime commands use the new `devenv-android` config path with legacy fallback.
- **Status**: v0.2.4 on `main`

## Immediate Context

`devenv-android` remains the Android entry layer for `dev-vm`.
The main project-entry drift was reduced in the previous slice, and the remaining
runtime-boundary drift is closed here.

What changed:

- `op` now opens existing projects with `devenv open <repo>`
- `np` now uses `newproj` only for repo/bootstrap work and then enters
  `devenv open <repo>`
- the mobile client no longer asks `newproj` to create `proj_*` tmux sessions
- `op`, `np`, and `install.sh` now fail clearly outside Termux instead of acting
  as an undocumented second client mode

This keeps repo creation in `devenv-bootstrap` while moving workspace entry back to the
core owner of workspace semantics.

Post-rebrand cleanup now also aligns config paths: `install.sh` creates
`~/.config/devenv-android/config`, and runtime commands prefer that path while
falling back to `~/.config/termux-client/config` for existing installs.

## Active Files

| File | State |
|------|-------|
| `README.md` | Updated - explicit that the repo is Termux/Android-only and points desktop users elsewhere |
| `CHANGELOG.md` | Updated - records canonical `devenv` convergence and the boundary clarification |
| `LLM_START_HERE.md` | New - contributor and governance rules |
| `docs/PROJECT_CONTEXT.md` | Updated - repo role and runtime boundary clarified |
| `docs/STRUCTURE.md` | New - repo layout |
| `docs/VERSIONING_RULES.md` | New - version policy |
| `docs/llm/HANDOFF.md` | Updated - current state and boundary decisions |
| `docs/llm/HISTORY.md` | New - append-only session record |
| `docs/llm/DECISIONS.md` | Updated - stable rationale |
| `scripts/check-version-sync.sh` | New - marker drift validation |
| `scripts/bump-version.sh` | New - atomic version marker updates |
| `scripts/pre-commit-hook.sh` | New - commit guardrail template |
| `bin/op` | Modified - Termux-only wrapper for project selection and `devenv open` |
| `bin/np` | Modified - Termux-only wrapper for repo bootstrap then `devenv open` |
| `bin/bootstrap-phone` | Modified - now seeds `~/src` and describes `devenv`-based mobile entry |
| `bin/doctor-phone`, `bin/vscode-web` | Modified - prefer new `devenv-android` config/cache paths with legacy fallback |
| `install.sh` | Modified - Termux-only installer with explicit failure on unsupported environments and legacy config migration |

## Current Version

- **devenv-android**: 0.2.4

## Top Priorities

1. Keep the new `devenv`-based mobile entry stable inside the supported Termux runtime
2. Keep bootstrap/docs aligned with the supported Termux-only workflow
3. Validate the converged flow on a real Android device
4. Keep stack-level docs in `home-infra` aligned with any future change here

## Key Decisions

- D-001: `devenv-android` is a client layer, not the owner of workspace semantics
- D-002: establish governance before changing the mobile workflow
- D-003: use `newproj` for repo/bootstrap work, but `devenv` for workspace entry
- D-004: `devenv-android` is Termux-only; desktop/local-shell use belongs elsewhere
- D-005: `devenv-android` is the Android client layer of the devenv-stack

## Do Not Touch

- The new `devenv`-based entry flow without coordinating docs/bootstrap changes
- Host/config conventions in `~/.config/devenv-android/config` and the legacy
  `~/.config/termux-client/config` fallback without checking docs and bootstrap implications
- The Termux-only runtime boundary unless the product scope is explicitly widened

## Open Questions

- Should `op` / `np` keep opening `code-server` automatically, or should project entry and browser entry become separate choices?

## Testing Notes

- v0.2.4 validation: `scripts/check-version-sync.sh` passes for 0.2.4; shell syntax passes for `bin/op`, `bin/np`, `bin/bootstrap-phone`, `bin/doctor-phone`, `bin/vscode-web`, and `install.sh`. Real Android smoke remains pending.

- No automated tests exist yet
- Syntax validated with `bash -n` for `bin/op`, `bin/np`, `bin/bootstrap-phone`, and `install.sh`
- Negative-path validation should confirm `op`, `np`, and `install.sh` now reject non-Termux execution
- Mocked command-capture validation should confirm:
  - `op` now builds SSH -> `devenv open <repo>`
  - `np` now builds SSH -> `newproj <repo> private && devenv open <repo>`
- Governance validation for this slice should use `scripts/check-version-sync.sh`

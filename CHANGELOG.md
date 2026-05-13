## [0.2.4] - 2026-05-13

### Added

### Changed

### Fixed

## [0.2.4] - 2026-05-13

### Added

### Changed

- `op`, `np`, `doctor-phone`, `bootstrap-phone`, and `vscode-web` now prefer `~/.config/devenv-android/config`, matching `install.sh`.
- `install.sh` copies an existing legacy `~/.config/termux-client/config` into the new config path on first run.
- `vscode-web` now prefers `~/.cache/devenv-android/vscode-tunnel.pid` while preserving fallback to the legacy tunnel pid file.

### Fixed

- Fixed the post-rebrand config-path mismatch where a fresh install created `~/.config/devenv-android/config` but runtime commands still loaded `~/.config/termux-client/config`.
- Fixed the non-Termux installer guidance to point desktop users at `devenv` instead of the old `tmux-workspace` name.

## [0.2.3] - 2026-05-13

### Added

- D-005 in `docs/llm/DECISIONS.md` records this repo as the Android client layer of the devenv-stack (canonical doc: `~/src/home-infra/docs/DEVENV_STACK.md`) and part of ForgeOS's operator-toolbox ecosystem model.

### Changed
- Cleaned remaining post-rebrand docs references from `tmux-workspace` / `dev-tools` to `devenv` / `devenv-bootstrap`.

### Fixed

## [0.2.2] - 2026-05-13

### Added

### Changed

- Repo renamed from `termux-client` to `devenv-android` as part of the devenv-stack rebrand (canonical doc: `~/src/home-infra/docs/DEVENV_STACK.md`). Internal references updated to the new name. `~/.config/termux-client/config` and `~/.cache/termux-client/` paths preserved for compatibility with existing Termux installs; migration of config paths to the new name is deferred to a follow-up release.
- Error messages now identify the binary as `devenv-android/op`, `devenv-android/np`, etc.

### Fixed

## [0.2.1] - 2026-03-19

### Added

### Changed

- `op`, `np`, and `install.sh` are now explicitly supported only inside Termux on Android
- README and working-memory docs now point desktop/local-shell users to plain SSH or the `devenv` desktop client
- Removed the leftover duplicated launch heading in the README

### Fixed

- Closed the remaining product-boundary drift where `devenv-android` still behaved like an undocumented second desktop/local-shell client

## [0.2.0] - 2026-03-18

### Added

- Clear host-side dependency checks in `op` and `np` for `devenv` and `newproj`

### Changed

- `op` now opens existing repos through the canonical `devenv open <repo>` flow
- `np` now uses `newproj` only for repo creation/bootstrap, then enters the canonical `devenv` workspace with `devenv open <repo>`
- Mobile project entry no longer asks `newproj` to create `proj_*` tmux sessions
- `bootstrap-phone` now seeds the canonical remote workspace root at `~/src` and describes the new `devenv`-based mobile flows

### Fixed

- Removed the biggest current workflow drift in the Android client by aligning project entry with the core `dev_*` model

## [0.1.0] - 2026-03-18

### Added

- Governance and versioning scaffold for the existing Android client repo
- LLM handoff/history/decision files for future stack-alignment work

### Changed

- Established `devenv-android` as a governed client-layer repo in the wider
  `devenv` stack

### Fixed

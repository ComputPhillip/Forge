# Changelog

All notable changes to Forge are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), versioning follows [SemVer](https://semver.org/).

## [Unreleased]

### Planned

- Deep internal rename of `hermes_cli/` → `forge_cli/` and related package directories
- Migration of `HERMES_*` environment variables to `FORGE_*` (with deprecated-alias compatibility shim during the transition)
- Plugin path consolidation under `plugins/forge-*`
- Updated install scripts hosted from Forge's own URLs
- First substantive divergent design choice (TBD — currently identifying candidates)

## [0.1.0] — 2026-05-25

### Added

- **Fork established.** Forge is born as a community fork of [hermes-agent](https://github.com/NousResearch/hermes-agent) at commit `e3236e99a40b84709d8bdd255136c1af8fb91aee` (branch `feature/seeded-codex-harness`).
- `NOTICE` file documenting the fork point and upstream attribution.
- `README.md` rewritten with Forge identity, clear acknowledgment of upstream, "Early Fork" status badge.
- `pyproject.toml` package name changed from `hermes-agent` to `forge`. Version reset to `0.1.0`.
- New CLI entry points: `forge`, `forge-agent`, `forge-acp` (alongside preserved `hermes`, `hermes-agent`, `hermes-acp` aliases for backward compatibility during the surface-rebrand transition).
- New `FORGE_LOGO` ASCII art in the startup banner, using the same gold/bronze gradient as the upstream HERMES logo so users see visual continuity.
- Banner version label now reads `Forge v0.1.0 (engine: hermes-agent vX.Y.Z, YYYY-MM-DD)` — honest about the fork relationship and the underlying engine version.

### Preserved

- Original `LICENSE` (MIT, © 2025 Nous Research) unchanged as required by the MIT license.
- All upstream functionality: this release is a surface rebrand only. The agent loop, tool surface, memory system, plugin ecosystem, model providers, terminal backends, gateway, and platform integrations all behave identically to the upstream fork point.
- All internal package names (`hermes_cli`, `hermes_constants`, `hermes_bootstrap`, etc.) and `HERMES_*` environment variables remain functional. The deep internal rename is deferred to a future release to avoid shipping a half-rebranded state.

### Known Limitations

- This release is **surface-only**. Code spelunkers will find the codebase is still organized under `hermes_*` package names. This is intentional — see `[Unreleased] / Planned` for the migration plan.
- Forge does not yet host its own install scripts, docs site, badge endpoints, or release artifacts. The README install instructions delegate to upstream for the bootstrap step.
- No divergent features yet. The value of being on Forge today is purely "you're following a fork in early development"; if you need stability or feature differentiation, upstream hermes-agent is the better choice.

### Attribution

The entire codebase below the surface-rebrand layer is the work of Nous Research and hermes-agent contributors over multiple years. Forge gratefully inherits all of it. See [LICENSE](LICENSE) and [NOTICE](NOTICE).

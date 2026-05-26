<p align="center">
  <img src="assets/forge-banner.svg" alt="Forge — a community fork of hermes-agent" width="100%">
</p>

# Forge ⚒

<p align="center">
  <a href="https://github.com/ComputPhillip/Forge/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License: MIT"></a>
  <a href="https://github.com/ComputPhillip/Forge"><img src="https://img.shields.io/badge/Status-Early%20Fork-orange?style=for-the-badge" alt="Status: Early Fork"></a>
  <a href="NOTICE"><img src="https://img.shields.io/badge/Based%20on-hermes--agent-blueviolet?style=for-the-badge" alt="Based on hermes-agent"></a>
</p>

> **What Forge is:** A community fork of [hermes-agent](https://github.com/NousResearch/hermes-agent) by [Nous Research](https://nousresearch.com), MIT-licensed, with upstream copyright preserved in [LICENSE](LICENSE) and fork attribution in [NOTICE](NOTICE).
>
> **What's actually different from hermes-agent right now:** Only the branding, the binary name (`forge` vs. `hermes`), and the maintainer. The agent runtime, tool surface, memory system, and plugin ecosystem are byte-identical to upstream commit `e3236e9`. **You are running hermes-agent.**
>
> **Why fork then:** To explore divergent design choices that wouldn't fit upstream — different defaults, leaner tool sets, opinionated rewrites. None of that is shipped in v0.1.0. For the full comparison and when-to-choose-which, see [Forge vs. hermes-agent](#forge-vs-hermes-agent) below.
>
> **For production today, use upstream [hermes-agent](https://github.com/NousResearch/hermes-agent).** It has a larger community, faster security response, and is what Forge is built on.

---

**The self-improving AI agent — Forge inherits hermes-agent's full capability set:** a built-in learning loop that creates skills from experience, improves them during use, nudges itself to persist knowledge, searches its own past conversations, and builds a deepening model of who you are across sessions. Runs on a $5 VPS, a GPU cluster, or serverless infrastructure that costs nearly nothing when idle. Not tied to your laptop — talk to it from Telegram while it works on a cloud VM.

Use any model you want — [Nous Portal](https://portal.nousresearch.com), [OpenRouter](https://openrouter.ai) (200+ models), [NovitaAI](https://novita.ai), [NVIDIA NIM](https://build.nvidia.com), [Xiaomi MiMo](https://platform.xiaomimimo.com), [z.ai/GLM](https://z.ai), [Kimi/Moonshot](https://platform.moonshot.ai), [MiniMax](https://www.minimax.io), [Hugging Face](https://huggingface.co), OpenAI, or your own endpoint. Switch with `forge model` — no code changes, no lock-in.

<table>
<tr><td><b>A real terminal interface</b></td><td>Full TUI with multiline editing, slash-command autocomplete, conversation history, interrupt-and-redirect, and streaming tool output.</td></tr>
<tr><td><b>Lives where you do</b></td><td>Telegram, Discord, Slack, WhatsApp, Signal, and CLI — all from a single gateway process. Voice memo transcription, cross-platform conversation continuity.</td></tr>
<tr><td><b>A closed learning loop</b></td><td>Agent-curated memory with periodic nudges. Autonomous skill creation after complex tasks. Skills self-improve during use. FTS5 session search with LLM summarization for cross-session recall. Compatible with the <a href="https://agentskills.io">agentskills.io</a> open standard.</td></tr>
<tr><td><b>Scheduled automations</b></td><td>Built-in cron scheduler with delivery to any platform. Daily reports, nightly backups, weekly audits — all in natural language, running unattended.</td></tr>
<tr><td><b>Delegates and parallelizes</b></td><td>Spawn isolated subagents for parallel workstreams. Write Python scripts that call tools via RPC, collapsing multi-step pipelines into zero-context-cost turns.</td></tr>
<tr><td><b>Runs anywhere, not just your laptop</b></td><td>Seven terminal backends — local, Docker, SSH, Singularity, Modal, Daytona, and Vercel Sandbox. Daytona and Modal offer serverless persistence — your agent's environment hibernates when idle and wakes on demand.</td></tr>
<tr><td><b>Research-ready</b></td><td>Batch trajectory generation, trajectory compression for training the next generation of tool-calling models.</td></tr>
</table>

---

## Status — Early Fork

`v0.1.0` is a **surface rebrand** of [hermes-agent](https://github.com/NousResearch/hermes-agent). Under the hood it is hermes-agent. For the full breakdown of what's different, what's planned, and when to use Forge vs. upstream, jump to [Forge vs. hermes-agent](#forge-vs-hermes-agent) below.

---

## Quick Install

> **Note:** Forge installation currently goes through the upstream installer because the fork hasn't published its own install scripts yet. Once Forge has divergent install needs, this section will be updated.

### Linux, macOS, WSL2, Termux

```bash
# Install upstream hermes-agent, then check out Forge over it
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
git clone https://github.com/ComputPhillip/Forge.git ~/forge
cd ~/forge && uv pip install -e .
```

### Windows (native, PowerShell) — Early Beta

```powershell
# Upstream installer first
iex (irm https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.ps1)
# Then clone Forge
git clone https://github.com/ComputPhillip/Forge.git C:\Users\$env:USERNAME\Forge
cd C:\Users\$env:USERNAME\Forge
uv pip install -e .
```

After installation:

```bash
forge              # start chatting (Forge CLI, formerly `hermes`)
```

---

## Getting Started

```bash
forge              # Interactive CLI — start a conversation
forge model        # Choose your LLM provider and model
forge tools        # Configure which tools are enabled
forge config set   # Set individual config values
forge gateway      # Start the messaging gateway (Telegram, Discord, etc.)
forge setup        # Run the full setup wizard (configures everything at once)
forge update       # Update to the latest Forge version
forge doctor       # Diagnose any issues
```

The `hermes` command is preserved as a backward-compatible alias during the fork transition. Both invoke the same binary.

---

## Forge vs. hermes-agent

### The honest version, in one paragraph

Forge is hermes-agent with the user-visible surface rebranded. The agent loop, tool surface, memory system, plugin ecosystem, model providers, terminal backends, gateway, and platform integrations are byte-for-byte identical to the upstream fork point at the time of `v0.1.0`. **If you use Forge today, you are running hermes-agent with a different name on the binary and a different banner at startup.** That's the starting state, not the destination — the point of forking is to give a maintainer space to make design choices that may not fit upstream, without forcing those choices on the upstream community.

### What's actually different right now

| Aspect | hermes-agent | Forge |
|---|---|---|
| **Project owner** | [Nous Research](https://nousresearch.com) — organization with a team | [ComputPhillip](https://github.com/ComputPhillip) — one maintainer, community fork |
| **CLI binary** | `hermes` | `forge` (and `hermes` kept as a backward-compat alias on both branches) |
| **Python packages** (`main`) | `hermes_cli/`, `hermes_constants.py`, etc. | Same as upstream — surface rebrand only |
| **Python packages** (`feat/deep-rename-py` branch) | — | `forge_cli/`, `forge_constants.py`, `forge_bootstrap.py`, `forge_state.py`, `forge_time.py`, `forge_logging.py` — migration in progress |
| **Environment variables** | `HERMES_*` (e.g. `HERMES_HOME`, `HERMES_API_KEY`) | Still `HERMES_*` — migration to `FORGE_*` with a backward-compat shim is **planned, not shipped** |
| **Branding** | Hermes Agent identity by Nous Research | Forge identity. MIT-licensed. Clear upstream attribution in [LICENSE](LICENSE) and [NOTICE](NOTICE) |
| **Release cadence** | Frequent, by the Nous team | Slower, dependent on this fork's interests and one maintainer's time |
| **Bug fix response** | Large contributor community, fast security response | One maintainer, slower response, no dedicated security on-call |
| **Feature set** | What ships in hermes-agent | **Identical** in v0.1.0. May become a subset or superset later as Forge diverges |
| **Tests passing** | Maintained by upstream CI on every PR | Inherited; not yet re-verified end-to-end on Forge's CI |

Everything below the surface — the actual agent runtime — is unchanged from upstream commit [`e3236e99a40b84709d8bdd255136c1af8fb91aee`](https://github.com/NousResearch/hermes-agent/commit/e3236e99a40b84709d8bdd255136c1af8fb91aee). See [NOTICE](NOTICE) for the full fork attribution.

### What Forge intends to explore

This is the "why does this exist" part, and it's honest about being aspirational rather than shipped:

- **Sharper defaults.** Opinionated configuration choices for specific use cases (e.g., code-generation-first workflows, or fewer-but-deeper tools instead of "everything available").
- **Alternative tool surfaces.** Experimenting with smaller, leaner tool sets vs. hermes-agent's full ecosystem. Some of this work is being prototyped in a sibling [my-harness](https://github.com/ComputPhillip) project that comparatively benchmarks the lean-vs-rich tradeoff.
- **Harness ergonomics.** Different agent-loop conventions, different approaches to memory and context windows, different cost/latency tradeoffs.
- **Surgical changes that wouldn't fit upstream.** Opinionated rewrites that wouldn't be appropriate to propose against hermes-agent because they contradict its design goals or break compatibility for its broader user base.

**None of the above is shipped in v0.1.0.** The CHANGELOG and this section will be updated as each lands.

### When to choose Forge vs. hermes-agent

**Use upstream [hermes-agent](https://github.com/NousResearch/hermes-agent) if:**
- You need stability, broad community support, fast security response
- You want frequent releases and an active dependabot/CI/issue triage cadence
- You're putting this in production
- You want issues triaged within hours, not days

**Consider Forge if:**
- You're interested in the divergent design choices listed above (once they ship)
- You're contributing to this fork's experimental work
- You want a stable target that intentionally moves slower than upstream
- You want to follow this maintainer's specific direction

For nearly everyone today, **upstream hermes-agent is the right answer.** Forge will earn its differentiation over time or not at all. The README will be updated honestly either way.

### Contributing back vs. forking forward

A practical convention this fork tries to follow:

1. **If a fix is broadly useful** (security, correctness, portability, performance regression), it belongs upstream first. Open a PR against hermes-agent. The Forge tree should not become a competing dumping ground for fixes that everyone benefits from.
2. **If a change is intentionally divergent** (different defaults, different APIs, opinions hermes-agent has explicitly rejected), it belongs in Forge.
3. **If a change is uncertain**, default to upstream — it's harder to extract a feature from a fork later than to land it once.

### Acknowledgments

Nous Research built and maintains hermes-agent. Forge would not exist without their work. The MIT license at the root of this repository preserves their copyright unchanged, as required by MIT. If you find Forge useful, please also consider starring or supporting [hermes-agent](https://github.com/NousResearch/hermes-agent) — the underlying technology you're actually using.

---

## Contributing

Contributions to Forge are welcome under the same MIT license. Before opening a substantial PR:

1. Consider whether the change belongs upstream in hermes-agent first. If yes, please open the PR there as well or instead — that's the right home for fixes and broadly useful improvements.
2. Forge-specific changes (those that intentionally diverge from upstream behavior or branding) belong here.
3. Read [CONTRIBUTING.md](CONTRIBUTING.md) for the contribution workflow inherited from hermes-agent, which Forge follows.

---

## Attribution

Forge would not exist without [hermes-agent](https://github.com/NousResearch/hermes-agent) and the work of [Nous Research](https://nousresearch.com). The MIT license at the root of this repository preserves their copyright unchanged, as required. The [NOTICE](NOTICE) file documents the fork point and our relationship to upstream.

If you find Forge useful and want to support the underlying technology, please also consider supporting Nous Research's work on hermes-agent.

---

## License

MIT — see [LICENSE](LICENSE) for the full text. Original copyright © 2025 Nous Research. Contributions to Forge are also MIT-licensed.

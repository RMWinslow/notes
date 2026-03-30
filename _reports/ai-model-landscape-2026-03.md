# AI Model Landscape for Coding — March 2026

Report compiled during a Claude Code session on 2026-03-29/30. Findings are
based on web searches and may not be perfectly accurate; verify before acting
on any specific claim.

## Frontier Model Benchmarks (March 2026)

| Model | SWE-bench Verified | HumanEval | LiveCodeBench | Terminal-Bench |
|-------|-------------------|-----------|---------------|----------------|
| Claude Opus 4.6 | **80.8%** | 95.0% | 76.0% | 65.4% |
| Claude Sonnet 4.6 | 79.6% | — | — | — |
| GPT-5.4 | Not published | — | — | **75.1%** |
| Gemini 3.1 Pro | 78.0% | 93.0% | 81.3% | 56.2% |
| MiniMax-M2.5 | 80.2% | — | — | — |
| Kimi K2.5 (open) | 76.8% | **99.0%** | 85.0% | 50.8% |
| Qwen 3.5 (open) | 76.4% | — | **83.6%** | 52.5% |
| GLM-5 (open) | 77.8% | — | — | — |
| Step-3.5-Flash (open) | — | — | 86.4% | — |

Claude Opus 4.6 leads SWE-bench Verified (real GitHub issue resolution).
Open-source models have largely closed the gap, with multiple models above 76%.

## Thinking/Chain-of-Thought Transparency

This is one of the most significant divergences in the current model landscape.

### Full transparent CoT (you see the raw reasoning)

- **DeepSeek R1 / V3.1+ / V3.2** — "DeepThink" mode shows the full chain of
  thought. This is one of DeepSeek's signature features.
- **Qwen 3 / 3.5** — Built-in "thinking" and "non-thinking" modes toggled at
  the API level. Uses `<think>` blocks.
- **Kimi K2.5** — Fully transparent always-thinking mode.
- **GLM-4.7 / GLM-5** — "Interleaved reasoning" woven into the output.
- **Claude Sonnet 3.7** — The one Claude model that returns full unabridged
  thinking via the API. No longer the frontier model.
- **All open-source reasoning models** — Full CoT by definition, since you
  control the inference.

### Summarized / hidden CoT

- **Claude 4 models (Opus 4.6, Sonnet 4.6)** — The API returns summarized
  thinking by default. Full thinking is only available to enterprise customers
  who contact Anthropic's sales team. The API docs say: "In rare cases where
  you need access to full thinking output for Claude 4 models, contact our
  sales team." Users are billed for the full thinking tokens regardless.
- **OpenAI o-series (o1, o3) and GPT-5.4** — Reasoning tokens are never
  exposed. Only a summary is shown. OpenAI's stated reason is safety.
- **Gemini 2.5 Pro+** — Recently moved from full to summarized thinking,
  following the same trajectory as Claude.

### Claude Code specifically

Claude Code has had a troubled history with thinking visibility:

- **v2.0.8**: Thinking summaries were visible.
- **v2.0.9** (Oct 2025): Thinking transcript removed.
- **v2.1.69** (Mar 2026): Claude Code began sending an undocumented
  `redact-thinking-2026-02-12` beta header that strips thinking entirely.
- **Workaround**: Adding `"showThinkingSummaries": true` to
  `~/.claude/settings.json` prevents the redact header and restores summaries.
  Discovered by users reverse-engineering the minified source code
  (GitHub issue #31326).
- **Feature request to show thinking (#9099)**: Closed by an automated bot as
  "not planned." Users pointed out the bot was known to be buggy.

### Key references

- GitHub issue #8477 — 183+ upvotes requesting visible thinking in Claude Code
- GitHub issue #31326 — The `showThinkingSummaries` workaround
- GitHub issue #9099 — Closed as "not planned" by bot

## Subscription Pricing Comparison

### Anthropic (Claude)

| Tier | Price | Models | Coding tool |
|------|-------|--------|-------------|
| Free | $0 | Sonnet | Claude Code (limited) |
| Pro | $20/mo | Opus 4.6, Sonnet 4.6 | Claude Code (full) |

### OpenAI (ChatGPT / Codex)

| Tier | Price | Models | Coding tool |
|------|-------|--------|-------------|
| Free | $0 | GPT-5.3 (limited, ads) | — |
| Go | $8/mo | GPT-5.3 (more messages, ads) | — |
| Plus | $20/mo | Full suite | Codex (30-150 msgs/5hr) |
| Pro Lite | $100/mo | Premium models | Codex (higher limits) |
| Pro | $200/mo | Premium models | Codex (300-1500 msgs/5hr) |

OpenAI never shows reasoning tokens at all — worse than Claude for
transparency. Codex has per-window message caps.

## Open-Source Coding Agents

Several open-source tools compete with Claude Code:

- **Cline** — 5M+ installs across VS Code, Cursor, JetBrains, Zed, and
  Neovim. Added native subagents and CLI 2.0 with headless CI/CD mode in
  February 2026.
- **OpenCode** — Terminal-based, multi-session, compatible with 75+ models.
  Privacy-first (no code stored externally). Directly positioned as a Claude
  Code alternative.
- **Aider** — Open-source CLI tool. Works with multiple model backends.
  Shows whatever the API returns.
- **Roo Code** — Plans, writes, and fixes code across multiple files.
- **Goose** (Block/Square) — CLI-first agent framework for automation/DevOps.

## Running Models Locally

### Kimi K2.5

- ~1 trillion total parameters, 32B active (MoE)
- Minimum ~150-250 GB memory even at aggressive quantization
- Not practical on consumer hardware
- Cheapest local path: Mac Studio M4 Ultra with 192+ GB (~$5-7K)

### Qwen3-Next-80B-A3B

- 80B total, only 3B active parameters
- At Q4 quantization: ~45 GB total (VRAM + RAM)
- Runs on a single RTX 4090 or 64 GB MacBook
- Community reports ~122 tok/s on RTX 4090
- Full transparent thinking via `<think>` blocks

### DeepSeek R1 distills

- DeepSeek-R1-Distill-Qwen3-8B: 8B parameters, full CoT
- Runs easily on consumer hardware
- 87.5% on AIME 2025

## Cross-Tool Configuration Standards

### AGENTS.md

AGENTS.md is an emerging cross-tool standard for project instructions,
stewarded by the Agentic AI Foundation under the Linux Foundation. It is
supported by OpenAI Codex, Cursor, Amp, and other tools.

Claude Code does NOT read AGENTS.md natively (only CLAUDE.md). Multiple
feature requests with thousands of upvotes have been filed:
- GitHub issue #6235 (Aug 2025)
- GitHub issue #34235
- GitHub issue #31005

**Workaround**: Add an instruction in the global `~/.claude/CLAUDE.md` to
read `AGENTS.md` if it exists. We implemented this on 2026-03-30.

### MCP (Model Context Protocol)

MCP is a standard protocol for AI tools to connect to helper programs that
provide additional capabilities (database access, email, web browsing, etc.).
Both Claude Code and OpenAI Codex support MCP, so MCP server configurations
transfer between tools.

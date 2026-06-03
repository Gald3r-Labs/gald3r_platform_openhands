# gald3r Readiness Report — OpenHands

> An honest accounting of how much of the gald3r framework installs natively on this
> platform, what degrades to an approximation, and what has no native home yet.
> Generated from a live documentation crawl on 2026-06-02.

**Overall readiness: ✅ Full.** OpenHands (All Hands AI, formerly OpenDevin) ships a composable
Software Agent SDK with CLI / GUI / Cloud surfaces. All six gald3r-relevant extension
mechanisms — commands, rules, agents, skills, hooks, and MCP — map onto native primitives,
and Plugins bundle the entire set into a single redistributable package.

## C.R.A.S.H. capability grid

| | Capability | Native? | What gald3r gets here | The gap |
|---|---|:---:|---|---|
| **C** | Commands | ✅ | Custom slash commands via plugin `commands/<name>.md`; Skills surface as `/skill-name`; a slash-command menu lists both | No standalone per-repo command file outside Plugins/Skills — slash-menu surfacing only landed in the May 2026 update |
| **R** | Rules | ✅ | `AGENTS.md` (repo root, always-on, injected at conversation start); General Skills load continuously; `GEMINI.md` / `CLAUDE.md` variants recognized | None — gald3r rules load here as first-class always-on instruction files |
| **A** | Agents | ✅ | File-based agents (`.agents/agents/*.md`, name/description/tools/model frontmatter) plus `register_agent()` factories and `DelegateTool` sub-agent spawning | Advanced multi-agent roles (factories, parallel `DelegateTool` orchestration, custom tools) are SDK/Python-level, not file-declarative |
| **S** | Skills | ✅ | Agent Skills — `SKILL.md` (extended AgentSkills standard) under `.agents/skills/`; keyword-trigger, `invoke_skill()`, or always-on modes | None for install — but directory conventions are mid-migration (`.agents/` recommended vs deprecated `.openhands/` paths) |
| **H** | Hooks | ✅ | Six lifecycle events (`PreToolUse`, `PostToolUse`, `UserPromptSubmit`, `Stop`, `SessionStart`, `SessionEnd`) via `.openhands/hooks.json`; JSON stdin payload, deny/allow decisions | None — a true deterministic control layer comparable to Claude Code hooks; works across Cloud / CLI / GUI |

_Legend: ✅ native · ⚠️ partial / approximated · ❌ no native mechanism · ❓ unverified_

**Beyond C.R.A.S.H. — MCP: ✅** Native Model Context Protocol via `config.toml [mcp]`,
Settings > MCP UI, or plugin `.mcp.json` — stdio, SSE, and SHTTP transports, per-tool
timeouts, API-key and OAuth auth. gald3r's MCP backend connects directly.

## Adoptable extras (non-C.R.A.S.H.)

Platform-native strengths gald3r can lean on, and which need wiring:

| Feature | Status | gald3r fit |
|---|:---:|---|
| Plugins (bundle skills/hooks/MCP/agents/commands into one package) | ✅ present | The ideal gald3r packaging target — one plugin carries the entire gald3r primitive set |
| Extended AgentSkills `SKILL.md` standard | ✅ present | Strong cross-tool portability between OpenHands and other AgentSkills tools (TRAE, CodeBuddy, etc.) |
| OpenHands Software Agent SDK (V1, Apache-2.0, LiteLLM) | ⚙️ needs customization | Custom tools, visualizers, and the `AgentFactory` registry make gald3r tooling extensible in code |
| Multi-surface config (CLI / GUI / Cloud / Enterprise; ACP via Zed) | ✅ present | Same gald3r install applies everywhere; no per-surface rework |

## The ceiling, and what's beyond it

gald3r runs at full strength on this platform — commands, rules, agents, skills, and hooks all map onto native mechanisms, so the framework installs without compromise. As third-party adaptation goes, this is the high end: nothing here has to be approximated.

But adaptation, however clean, is still gald3r living as a guest inside someone else's tool. The native build goes further — **gald3r_agent**, running on the **gald3r throne** over the **gald3r_world_tree** — where these primitives aren't mapped onto a host, they *are* the substrate. Same framework, no host in between.

> ### gald3r_agent — coming soon. 🌳

---

<sub>Capabilities verified against the platform's official documentation on 2026-06-02, and
re-verified each release via the gald3r platform-docs crawl. This report describes gald3r's
third-party adaptation surface; it is not an endorsement or critique of the platform itself.</sub>

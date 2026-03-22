## TL;DR

| | **GSD** | **BMAD-METHOD** | **Spec Kit** | **Agent OS** |
|---|---|---|---|---|
| **Core idea** | Context engineering for reliable AI coding | Agile methodology with specialized agents | Spec-driven dev workflow | Standards discovery & injection |
| **Target user** | Solo devs / indie hackers | Teams, enterprise | Any developer | Professional devs |
| **Complexity** | Low — opinionated, minimal | High — full agile lifecycle | Medium — structured but clear | Low — focused utility |
| **Primary problem solved** | Context rot in long AI sessions | Lack of structure in AI-assisted dev | Vibe coding → predictable outcomes | Agents ignoring your codebase patterns |
| **Agent style** | Sub-agent orchestration (planning/execution/verify) | 12+ role-based specialist agents (PM, Architect, SM…) | Linear workflow commands | Standards deployment + spec shaping |
| **Install** | `npx get-shit-done-cc` | `npx bmad-method install` | `uv tool install specify-cli` (Python) | Scripts/commands install |
| **AI platforms** | Claude Code, Cursor, Copilot, Gemini, Codex, OpenCode | Claude Code, Cursor, others | Claude Code, Copilot, Codex, Kiro, Amp, Qoder | Claude Code, Cursor, Antigravity |
| **Output artifacts** | `PROJECT.md`, `REQUIREMENTS.md`, `ROADMAP.md`, `PLAN.md`, `STATE.md` | Stories, epics, architecture docs, test plans | `constitution.md`, `spec.md`, `plan.md`, `tasks.md` | `standards/`, `spec.md` |

## Platform Support

| | **GSD** | **BMAD-METHOD** | **Spec Kit** | **Agent OS** |
|---|---|---|---|---|
| **Claude Code** | ✅ Native — `.claude/commands/gsd/`, slash commands `/gsd:*` | ✅ Native — skills into `.claude/`, invoked as `bmad-help` etc. | ✅ Native — `.claude/commands/`, slash commands `/speckit.*` | ✅ Native — `.claude/commands/agent-os/`, slash commands `/agent-os:*` |
| **Cursor** | ✅ Native — `.cursor/`, same `/gsd:*` commands | ⚠️ Mentioned, but don't see specific | ✅ Native — `.cursor/commands/` via `cursor-agent` CLI | ⚠️ Mentioned, but don't see specific |
| **OpenCode** | ✅ Native — `~/.config/opencode/`, commands use `/gsd-help` prefix | ⚠️ Mentioned, but don't see specific | ✅ Native — `.opencode/command/` (singular dir name) | ❌ Not mentioned |
| **Windsurf** | ❌ Not mentioned | ❌ Not mentioned | ✅ Native — `.windsurf/workflows/`, IDE workflow format | ⚠️ Mentioned, but don't see specific |

## Deep Dive

### 1. GSD (SDD)
- **Philosophy**: Anti-enterprise. Built by a solo dev for solo devs. Solves *context rot* — the degradation as Claude's context window fills up.
- **How it works**: You describe your idea → GSD extracts full requirements → creates roadmap → phases → atomic task plans → executes in fresh sub-contexts. Each plan is small enough to run in a clean window.
- **Unique strengths**: Context window management (the core differentiator), parallel sub-agent execution, model profile switching (quality/balanced/budget), security hardening, backlog management.
- **Weakness**: Opinionated workflow — not designed for large teams or complex enterprise org structures.

### 2. BMAD-METHOD (Methodology + SDD)
- **Philosophy**: "AI-driven Agile." Structured like a real software team — you work *with* specialist agents (PM, Architect, Developer, UX, Scrum Master…) not just one chat-bot.
- **How it works**: You go through full agile lifecycle — brainstorm → PRD → architecture → stories → dev loop. "Party Mode" lets you bring multiple agent personas into one session.
- **Unique strengths**: Scale-adaptive (adjusts depth based on project complexity), modular ecosystem (game dev, testing, creative intelligence modules), the most comprehensive lifecycle coverage, 34+ workflows, completely free.
- **Weakness**: Heavy. Most complex of the four. Overkill for solo indie projects or quick features.

### 3. Spec Kit (SDD)
- **Philosophy**: "Specs become executable." Flip the traditional approach — spec first, code second. Backed by GitHub itself.
- **How it works**: `constitution` → `specify` → `clarify` → `plan` → `tasks` → `implement`. Each step is a CLI command that creates structured documents. Strong emphasis on *clarification before planning* to reduce rework.
- **Unique strengths**: GitHub-backed credibility, Python-based CLI (`uv`), supports the widest range of AI agents (Copilot, Kiro, Amp, Qoder, etc.), excellent brownfield/existing codebase support, `presets` and `extensions` for customization.
- **Weakness**: More manual/collaborative — doesn't do as much automatic orchestration. Requires more active steering from the developer.

### 4. Agent OS (SDD)
- **Philosophy**: Solve the root cause of why agents produce inconsistent code — **they don't know your standards**. The narrowest scope of the four.
- **How it works**: `discover-standards` → extract patterns from your existing codebase → `deploy-standards` → intelligently inject relevant standards into agent context based on what you're building. Plus `shape-spec` for better planning.
- **Unique strengths**: Laser-focused on the standards problem. Works *alongside* other tools (you could use Agent OS + GSD or Agent OS + Spec Kit together). Extremely lightweight.
- **Weakness**: Not a full development workflow — it's a complement, not a replacement. No lifecycle management, no phased execution.

## Key Differentiators

| Concern | Best Tool |
|---|---|
| Context rot / long sessions | **GSD** |
| Team collaboration, full agile | **BMAD** |
| Spec quality & clarification | **Spec Kit** |
| Agent consistency with your codebase | **Agent OS** |
| Widest AI platform support | **Spec Kit** |
| Least overhead for solo devs | **GSD** or **Agent OS** |
| Most customizable | **BMAD** (module ecosystem) |

## How They Relate to Each Other

They solve adjacent but distinct problems and are **not direct competitors**. A reasonable stack could be:

> **Agent OS** (discover your standards) + **GSD** (execute phases reliably) + **Spec Kit** (write quality specs before starting)

GSD's author explicitly mentions Spec Kit and BMAD as "more complicated than needed." BMAD is the most mature/comprehensive. Spec Kit is the most GitHub-ecosystem-native. Agent OS is the most focused utility.

## References

[GSD](https://github.com/gsd-build/get-shit-done)

[BMAD](https://github.com/bmad-code-org/BMAD-METHOD)

[SpecKit](https://github.com/github/spec-kit)

[SpecKit in Action](https://github.com/mduongvandinh/spec-kit-docs)

[Agent OS](https://github.com/buildermethods/agent-os)

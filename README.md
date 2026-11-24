# The Monte Carlo Method

An [Agent Skill](https://agentskills.io) that gives coding agents an engineering discipline: build the simplest coherent system that fulfills the actual contract, make intent obvious and complexity accountable, verify results, let evidence outrank authority, and leave the workspace and version history in good order.

It covers understanding and challenging the contract, justified complexity, plain and declarative APIs, acyclic module organization, behavior-focused tests, surgical changes, measurement you can trust, and work among independent, fallible agents: roles, bounded delegation, independent review, compute spent in proportion to risk, convergence, and turning lessons into lasting tests, specifications and rules. Read the full skill in [`skills/monte-carlo-method/SKILL.md`](skills/monte-carlo-method/SKILL.md).

It also ships an **orchestrator** agent, [`agents/orchestrator.md`](agents/orchestrator.md), that runs on the skill and answers for the result: every task it accepts ends either verified by evidence it has re-checked itself, or honestly unfinished. It adds the orchestrator's own practice (framing, staffing, briefing, verifying, deciding, integrating) without repeating the skill.

## Install

### Any agent (recommended)

The [`skills`](https://github.com/vercel-labs/skills) CLI detects your installed agents (Claude Code, OpenCode, Codex, Cursor, GitHub Copilot, Gemini CLI, and many more) and installs the skill into each:

```sh
npx skills add sharkkhq/monte-carlo-method
```

### Claude Code plugin

```
/plugin marketplace add sharkkhq/monte-carlo-method
/plugin install monte-carlo-method@monte-carlo-method
```

### Manual

Copy the `skills/monte-carlo-method` folder into your agent's skills directory:

| Agent | User-wide | Per-project |
| - | - | - |
| Claude Code | `~/.claude/skills/` | `.claude/skills/` |
| OpenCode | `~/.config/opencode/skills/` | `.opencode/skills/` |
| Agents that follow the shared `.agents` convention (e.g. Codex) | `~/.agents/skills/` | `.agents/skills/` |

```sh
git clone https://github.com/sharkkhq/monte-carlo-method
cp -r monte-carlo-method/skills/monte-carlo-method ~/.claude/skills/
```

### The orchestrator agent

The Claude Code plugin installs it automatically. Elsewhere, copy `agents/orchestrator.md` into your agent directory. It needs the skill installed too.

| Agent | User-wide | Per-project |
| - | - | - |
| Claude Code | `~/.claude/agents/` | `.claude/agents/` |
| OpenCode | `~/.config/opencode/agents/` | `.opencode/agents/` |

In OpenCode it can run as the primary agent or as a subagent. In Claude Code, start a session with `claude --agent orchestrator`, or delegate to it from another session.

### Agents without skill support

Paste the body of `SKILL.md` (everything after the frontmatter) into the agent's instructions file, such as `AGENTS.md`, `CLAUDE.md`, `.github/copilot-instructions.md`, or a Cursor rule.

## Usage

Agents load the skill automatically when designing, implementing, refactoring, reviewing, or testing software. You can also ask for it by name, e.g. "use the monte-carlo-method skill". Choose the orchestrator agent for work you want split across several agents and integrated.

## License

[MIT](LICENSE)

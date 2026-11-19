# The Monte Carlo Method

An [Agent Skill](https://agentskills.io) that gives coding agents an engineering discipline: build the simplest coherent system that fulfills the actual contract, make intent obvious and complexity accountable, verify results, and leave the workspace and version history in good order.

It covers understanding before acting, justified complexity, plain and declarative APIs, acyclic module organization, behavior-focused tests, surgical changes, measured performance work, and stewardship across subagents. Read the full skill in [`skills/monte-carlo-method/SKILL.md`](skills/monte-carlo-method/SKILL.md).

## Install

### Any agent (recommended)

The [`skills`](https://github.com/vercel-labs/skills) CLI detects your installed agents (Claude Code, OpenCode, Codex, Cursor, GitHub Copilot, Gemini CLI, and many more) and installs the skill into each:

```sh
npx skills add splashsky/monte-carlo-method
```

### Claude Code plugin

```
/plugin marketplace add splashsky/monte-carlo-method
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
git clone https://github.com/splashsky/monte-carlo-method
cp -r monte-carlo-method/skills/monte-carlo-method ~/.claude/skills/
```

### Agents without skill support

Paste the body of `SKILL.md` (everything after the frontmatter) into the agent's instructions file, such as `AGENTS.md`, `CLAUDE.md`, `.github/copilot-instructions.md`, or a Cursor rule.

## Usage

Agents load the skill automatically when designing, implementing, refactoring, reviewing, or testing software. You can also ask for it by name, e.g. "use the monte-carlo-method skill".

## License

[MIT](LICENSE)

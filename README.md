# The Monte Carlo Method

An [Agent Skill](https://agentskills.io) that gives coding agents an engineering discipline: build the simplest coherent system that fulfills the actual contract, make intent obvious and complexity accountable, verify results, let evidence outrank authority, and leave the workspace and version history in good order.

It covers understanding and challenging the contract, justified complexity, plain and declarative APIs, acyclic module organization, behavior-focused tests, surgical changes, measurement you can trust, and work among independent, fallible agents: roles, bounded delegation, independent review, compute spent in proportion to risk, convergence, and turning lessons into lasting tests, specifications and rules. Read the full skill in [`skills/monte-carlo-method/SKILL.md`](skills/monte-carlo-method/SKILL.md).

It also ships three agents that run on the skill, in [`agents/`](agents/):

- **orchestrator** answers for the result: every task it accepts ends either verified by evidence it has re-checked itself, or honestly unfinished. It adds the orchestrator's own practice (framing, staffing, briefing, verifying, deciding, integrating).
- **implementer** owns one bounded task, changes only what its brief grants, and reports evidence the orchestrator can re-check. It does not delegate, and leaves version control to the orchestrator.
- **reviewer** judges a change against its contract, independently of the implementer's account. It reproduces the verification, tries to break the change, and returns a verdict with evidence. It does not edit files or disturb the work tree.

Each adds only what its role needs on top of the skill: tool restrictions that guard against accidents (they are not a sandbox, so give an agent its own checkout when isolation matters), and the practice and report format a brief would otherwise repeat. None sets a model, so the orchestrator can pick one to suit each task.

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

### The agents

The Claude Code plugin installs them automatically. Elsewhere, copy the files in `agents/` into your agent directory. They need the skill installed too.

| Agent | User-wide | Per-project |
| - | - | - |
| Claude Code | `~/.claude/agents/` | `.claude/agents/` |
| OpenCode | `~/.config/opencode/agents/` | `.opencode/agents/` |

In OpenCode the orchestrator can run as the primary agent or as a subagent; the implementer and reviewer run only as subagents. For an orchestrator running as a subagent to delegate in turn, raise `experimental.subagent_depth` to 2 in OpenCode's configuration (the default, 1, prevents subagents from starting their own). In Claude Code, start a session with `claude --agent orchestrator`, or delegate to it from another session.

### Agents without skill support

Paste the body of `SKILL.md` (everything after the frontmatter) into the agent's instructions file, such as `AGENTS.md`, `CLAUDE.md`, `.github/copilot-instructions.md`, or a Cursor rule.

## Usage

Agents load the skill automatically when designing, implementing, refactoring, reviewing, or testing software. You can also ask for it by name, e.g. "use the monte-carlo-method skill". Choose the orchestrator agent for work you want split across several agents and integrated.

## License

[MIT](LICENSE)

# AGENTS.md

Instructions for AI coding agents (Codex, Devin, Cursor, and other AGENTS.md-compatible tools) in this repository.

## Project skills

Skills are reusable specialized instructions, one per folder, defined in `SKILL.md` files with YAML frontmatter (`name`, `description`). This project uses the `.claude/skills/` folder — a Claude Code convention, but the content is portable Markdown + bash: **any agent should read the matching skill before executing the task it covers**.

Available skills:

- `.claude/skills/browser-harness/SKILL.md` — real browser control via CDP (clicking, typing, navigation, logged-in sessions, JS-rendered or bot-protected pages). **Read this file before any browser-interaction task.** Do not use it for plain HTTP fetches of public content — use `curl` for those.

## Project commands

Commands are reusable slash commands, one `.md` file per command in the `.claude/commands/` folder, with YAML frontmatter (`description`, `allowed-tools`). In Claude Code they are invoked as `/<name>` (subfolders become namespaces: `commands/git/squash-history.md` → `/git:squash-history`); other agents should read the file and follow its steps:

- `.claude/commands/git/squash-history.md` — rewrites the entire repository history into a single commit (full squash of `main`) and force pushes. **Destructive and irreversible** — always confirm with the user before running.

## Project agents

Agents are specialized subagent definitions (a persona + scope + instructions), one `.md` file per agent in the `.claude/agents/` folder. Before delegating a subtask to a specialized agent, read the corresponding definition:

- _No agents defined yet._ When you create one, list it here with a summary of when to use it.

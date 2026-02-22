# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ccll (Claude Code Language Learning) is a Claude Code plugin repository that can contain multiple plugins/skills. Currently it ships the **learn-along** plugin — a conversational language coaching skill for intermediate+ learners, focused on software engineering communication.

## Repository Structure

This is a pure-Markdown Claude Code plugin with no build step, no dependencies, and no tests.

- `.claude-plugin/plugin.json` — Plugin manifest (name, version, metadata)
- `agents/<name>.md` — Subagent definitions (frontmatter + system prompt)
- `skills/<name>/SKILL.md` — Skill definitions (frontmatter + orchestration logic)

Each skill in `skills/` has a corresponding agent in `agents/` with the same name. The skill orchestrates when/how to invoke the agent.

## Naming Convention

The repository name `ccll` is an umbrella for multiple plugins. Individual plugin/skill/agent names are independent of the repo name (e.g., `learn-along`). When adding a new plugin, ensure the name is consistent across `plugin.json`, `agents/<name>.md`, and `skills/<name>/SKILL.md`.

## Adding a New Plugin

1. Add agent definition: `agents/<name>.md`
2. Add skill definition: `skills/<name>/SKILL.md`
3. Update `plugin.json` if needed
4. Update `README.md` with usage instructions

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ccll (Claude Code Language Learning) is a Claude Code plugin marketplace repository containing multiple language learning plugins for software engineers. Currently it ships the **learn-along** plugin.

## Repository Structure

This is a pure-Markdown Claude Code plugin repo with no build step, no dependencies, and no tests.

```
.claude-plugin/marketplace.json          ← Marketplace manifest (lists all plugins)
plugins/<plugin-name>/
  .claude-plugin/plugin.json             ← Per-plugin manifest
  agents/<name>.md                       ← Subagent definitions (frontmatter + system prompt)
  skills/<name>/SKILL.md                 ← Skill definitions (frontmatter + orchestration logic)
```

Each skill in `skills/` has a corresponding agent in `agents/` with the same name. The skill orchestrates when/how to invoke the agent.

## Naming Convention

The repository name `ccll` is an umbrella for multiple plugins. Individual plugin names are independent of the repo name (e.g., `learn-along`). When adding a new plugin, ensure the name is consistent across its `plugin.json`, `agents/<name>.md`, and `skills/<name>/SKILL.md`.

## Adding a New Plugin

1. Create directory: `plugins/<name>/`
2. Add plugin manifest: `plugins/<name>/.claude-plugin/plugin.json`
3. Add agent definition: `plugins/<name>/agents/<name>.md`
4. Add skill definition: `plugins/<name>/skills/<name>/SKILL.md`
5. Register in `.claude-plugin/marketplace.json` `plugins` array
6. Update `README.md` with the plugin table and usage instructions

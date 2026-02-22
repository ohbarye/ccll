# ccll - Claude Code Language Learning

A [Claude Code plugin](https://docs.anthropic.com/en/docs/claude-code/plugins) that augments your everyday coding sessions with language coaching for intermediate+ learners.

## What It Does

When activated, a language coaching subagent analyzes each conversational exchange and appends brief coaching notes after Claude's normal response. The coaching focuses on:

- **Natural expressions** — how native speakers would phrase the same intent in a professional engineering context
- **Vocabulary highlights** — idiomatic phrases, technical collocations, and register guidance
- **Corrections** — fixes for genuine errors or unnatural phrasing (not nitpicks)

The coaching is tuned for software engineering communication: PR comments, Slack messages, standups, technical docs, and pair programming dialogue.

## Installation

**From terminal:**

```bash
claude plugin marketplace add ohbarye/ccll
claude plugin install learn-along@ccll
```

**From a Claude session:**

```bash
/plugin marketplace add ohbarye/ccll
/plugin install learn-along@ccll
```

## Usage

Activate with the slash command:

```
/learn-along en          # Target: English, native: auto-detect
/learn-along from:ja to:en  # Explicit native/target
/learn-along off         # Deactivate
```

Once active, every response includes a short coaching section (3-8 lines) after a `---` separator. Your technical workflow is never interrupted — coaching is always appended after the full technical response.

## Example

If you write in Japanese during a coding session:

> このPRのテストが落ちてるから原因を調べて

Claude responds with the technical answer first, then appends:

```
---

**Learn Along** (target: English)

**Your intent in English:**
> Can you investigate why the tests in this PR are failing?

**Key phrases:**
- テストが落ちてる → "the tests are failing" -- casual; in a PR comment prefer "CI is red"
- 原因を調べて → "investigate the root cause" -- or casually, "look into why"

**Register note:** On Slack: "CI is red on this PR, can you take a look?"
```

## What to Expect

After installation, the plugin is available in any Claude Code session. Run `/learn-along` to activate — no other configuration needed.

- Coaching appears after every response as a short section (3-8 lines) below a `---` separator
- Your technical workflow is never interrupted — coaching is always appended after the full technical response
- Coaching does not persist across sessions; run `/learn-along` again in each new session

## License

MIT

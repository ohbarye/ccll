---
name: learning-language
description: Augments normal Claude Code conversations with language learning coaching for intermediate+ learners. Activate with `/learning-language <target-lang>` (e.g., `/learning-language en`). A subagent analyzes each exchange and provides natural expressions, vocabulary highlights, and corrections. Deactivate with `/learning-language off`. Triggers on "learning-language", "language coach", or requests to practice a language during coding sessions.
---

# Learning Language - Conversational Language Learning

Augment everyday software engineering conversations with language coaching for intermediate+ learners.

## When to Use This Skill

- User runs `/learning-language` or `/learning-language <target-language>`
- User mentions wanting to practice a language during Claude Code sessions
- User says "learning language", "language coach", or similar

## Activation

When the user invokes `/learning-language`:

1. Parse arguments:
   - `/learning-language en` → target: English, native: auto-detect
   - `/learning-language from:ja to:en` → native: Japanese, target: English
   - `/learning-language` (no args) → target: English, native: auto-detect
   - `/learning-language off` → deactivate
2. Confirm activation with a brief message stating the configured languages.
3. From this point forward, after **every response**, invoke the `learning-language` subagent.

### Auto-Detection of Native Language

When native language is not explicitly specified:

1. Detect from the user's first non-target-language message after activation.
2. If the user only writes in the target language, ask once to confirm their native language.
3. Once detected, confirm: "Native language detected: [X]. Use `/learning-language from:<native> to:<target>` to adjust."

## Deactivation

When the user runs `/learning-language off` or says "stop language coaching":

1. Stop invoking the learning-language subagent.
2. Confirm deactivation.

## State

- Learning-language mode is active for the **current conversation session only**.
- If context becomes unclear after a long conversation, briefly check: "Learning Language is still active (target: English). Say `/learning-language off` to stop."
- Activation does **not** persist across sessions. The user must re-activate in new sessions.

## Execution Flow (Per Exchange)

**IMPORTANT**: Always complete the user's technical request fully before adding coaching.

### Step 1: Respond Normally

Process the user's request and provide your full technical response as usual.

### Step 2: Invoke the learning-language Subagent

Use the `Task` tool with `subagent_type: "learning-language"` and `model: "haiku"`. The subagent will classify the input and produce appropriate coaching output.

Provide in the prompt:

- The user's original message
- A brief summary of your response (not the full text if lengthy)
- The native language and target language
- The domain context (e.g., "debugging test failures", "PR review", "architecture discussion")

Example invocation:

```
Task tool call:
  subagent_type: "learning-language"
  model: "haiku"
  prompt: |
    Native: Japanese, Target: English
    Domain: debugging test failures

    User message:
    このPRのテストが落ちてるから原因を調べて

    Assistant response summary:
    Investigated test failures, found mock setup issue in auth_test.rb, fixed by updating the expected arguments.
```

### Step 3: Append the Coaching Output

Append the subagent's output at the end of your response after a `---` separator.

## Output Format

```
---

**Learning Language** (target: English)

[Subagent output here - varies by category]
```

## Guidelines

- **Never let coaching interfere with the primary task.** Technical response comes first.
- **Keep it brief.** 3-8 lines for the coaching section.
- **Intermediate+ level.** No basic grammar explanations. Focus on idiomatic usage, register, nuance, collocations, and technical vocabulary.
- **Software engineering context.** Prioritize expressions used in PRs, Slack, standups, and technical docs.
- **Natural, not textbook.** Favor how native speakers actually talk in professional settings.

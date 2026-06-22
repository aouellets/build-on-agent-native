# Contributing

This repo holds one reference-standard [Skill Me](https://skillme.dev) skill.
The bar is high on purpose: a skill's `description` is what decides whether it
fires at the right moment and stays quiet otherwise.

## What a skill is

One skill is a single `SKILL.md` file living in its own directory under
[`skills/`](skills/):

```
skills/<kebab-case-name>/SKILL.md
```

The file is YAML frontmatter followed by an imperative Markdown body:

```markdown
---
name: Build on Agent-Native
description: <trigger-precise, see below>
---

# Build on Agent-Native

<imperative body — tell the agent what to do, in order>
```

## Frontmatter rules

- **`name`** — Title Case, human-readable. Required, non-empty.
- **`description`** — required, non-empty, and **trigger-precise** (see the bar
  below). This is the single most important field.
- The **directory name must be the kebab-case of `name`** —
  `Build on Agent-Native` → `build-on-agent-native`. The validator enforces this:
  lowercase, every run of non-alphanumerics collapses to one hyphen, leading and
  trailing hyphens trimmed.

## Body rules

- Start with an **H1** (`# Skill Name`).
- Imperative voice: tell the agent what to do, in the order it should do it.
- **No placeholder content.** `TODO`, `TKTK`, `lorem`, `<placeholder>`, and
  `[fill…` are rejected by the validator.
- Author the body as final content. Don't summarize or stub.

## The trigger-precision bar

A description has to do two jobs: pull the skill in when it's the right tool, and
keep it out of the way when it isn't. Earn both.

- **Say when to use it, concretely** — a `Use when…` clause plus the literal
  phrases a user actually says (`"build an agent-native app"`, `"defineAction"`).
- **Say when *not* to use it** — explicit `Do NOT use …` cross-references that
  hand off to the right neighbour by name (e.g. skill-creator, MCP-builder).
- **Make it long enough to disambiguate.** Descriptions under 12 words rarely
  carry enough signal; the validator warns below that threshold.

Read [`skills/build-on-agent-native/SKILL.md`](skills/build-on-agent-native/SKILL.md)
as the worked example — it names its boundaries in both the `description` and a
closing `## Don't` section.

## Attribution discipline

This skill describes Builder.io's separately-licensed `@agent-native/core`
framework; it does not vendor that code. If you edit the body, keep framework
API claims grounded in the **version-matched package docs** (`pnpm action
docs-search …`), not memory, and keep the upstream MIT attribution intact in the
[README](README.md).

## Validate

```bash
npm install
npm run validate
```

Hard failures (non-zero exit, block merge): frontmatter with non-empty `name`
and `description`; a non-empty body with an H1 and no placeholder tokens; a
directory name matching the kebab-case of `name`. Soft warnings (printed, don't
block): a `description` under 12 words or missing a trigger cue. CI runs the same
validator on every push and pull request.

## Scope

This repo is **catalog content only**. Nothing here imports from or modifies the
live Skill Me MCP server or its tool signatures (`install_skill`,
`get_active_skills`, and the rest).

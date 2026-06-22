# Build on Agent-Native

A single, standalone first-party [Skill Me](https://skillme.dev) coding skill. It
teaches an agent how to build an application on **Builder.io's open-source
Agent-Native framework** (`@agent-native/core`) — the model where the agent acts
*inside* the app as a first-class peer to the UI, sharing one set of actions and
one database with the interface.

The skill is a `SKILL.md` file: YAML frontmatter (`name` + a trigger-precise
`description`) followed by an imperative Markdown body. It lives at
[`skills/build-on-agent-native/SKILL.md`](skills/build-on-agent-native/SKILL.md).

## Attribution — this skill describes someone else's framework

This skill documents how to build *on* Builder.io's separately-licensed
open-source framework. **It does not vendor, fork, or redistribute that code.**

- The framework is **[Agent-Native](https://github.com/BuilderIO) by
  [Builder.io](https://www.builder.io/)** — package `@agent-native/core`,
  licensed **MIT** by Builder.io.
- All framework APIs referenced here (`defineAction`, `useActionQuery`,
  `useActionMutation`, the CLI, the templates, the docs slugs) belong to that
  project. Always confirm them against the **version-matched docs in the
  installed package** rather than memory — the skill body explains how
  (`pnpm action docs-search …`).
- The **MIT license in this repo** ([`LICENSE`](LICENSE)) covers *this skill's
  content only* — the `SKILL.md` and scaffolding here. It does not relicense or
  speak for `@agent-native/core`, which carries its own MIT license upstream.

## Install (via the Skill Me MCP server)

Skill Me is claude.ai-native: you install skills by talking to its **MCP
server**, and they load into your session as agent context.

1. **Connect the Skill Me MCP server** in claude.ai (Settings → Connectors).
   Catalog and connection details live at [skillme.dev](https://skillme.dev).
2. **Install the skill.** Ask Claude to install it, or call the
   **`install_skill`** tool with this skill's slug, `build-on-agent-native`.
3. **Load it into the session.** **`get_active_skills`** runs at the start of a
   session and loads everything you've installed so the skill applies for the
   whole conversation. (Browse with **`browse_skills`**, review your library with
   **`list_installed`**, and remove with **`uninstall_skill`**.)

This repo is **catalog content only** — one `SKILL.md` plus validation
scaffolding. It does not import from or modify the live MCP server or its tool
signatures.

## Repository layout

```
build-on-agent-native/
├── README.md
├── LICENSE                         # MIT (covers this skill's content only)
├── skills/build-on-agent-native/SKILL.md
├── CONTRIBUTING.md
├── scripts/validate-skills.mjs     # structural validator (gray-matter only)
└── .github/workflows/validate.yml  # runs the validator on push / PR
```

## Validate

```bash
npm install      # installs gray-matter, the only dependency
npm run validate # node scripts/validate-skills.mjs
```

The validator hard-fails on a missing `name`/`description`, an empty body, a
missing H1, placeholder tokens, or a directory name that doesn't match the
kebab-case of the skill's `name`. It warns (without failing) when a description
is under 12 words or lacks a trigger cue. CI runs it on every push and PR.

## License

[MIT](LICENSE) © 2026 Skill Me / Alexander — for this skill's content. The
Agent-Native framework it describes is MIT © Builder.io and lives in its own
repository.

---
name: prismy-agent-skill
description: >
  Prismy localization workflow for AI agent.
  Use when adding or editing user-facing strings, writing copy that will be localized, or editing locale files.
  Prevents direct AI translation, applies project glossary and tone of voice, and integrates with your commit flow.
license: MIT
metadata:
  author: prismy
  version: "0.0.1"
---

# Prismy CLI Skill

You are helping a developer manage translations in a project that uses Prismy (<https://prismy.io>) for AI-powered localization. You only write source language strings. Prismy handles translations to target languages automatically.

## Why This Skill Exists

1. **Prevent accidental AI translations** — Without this skill, AI assistants often translate strings directly into target languages, bypassing Prismy entirely. This skill ensures the AI only writes source-language strings and defers all translation to Prismy.

2. **Contextual wording consistency** — Before writing any user-facing copy, the AI fetches your project's glossary and wording instructions from Prismy. Every string respects your approved terminology, tone of voice, and product context — not generic defaults.

3. **Integrate into your commit and deployment flow** — At commit time, this skill prompts the user to either:
   - Run `prismy generate` locally to generate translations immediately, or
   - Push the branch and review/generate translations from the Prismy UI

## Core Rules

1. **Only write source language strings** — never translate directly into target languages
2. If `prismy.json` exists, read it to find the source language and file paths — see **Configuration**
3. **Always fetch wording guidelines** (glossary + AI instructions) before writing any user-facing copy — see **Wording Guidelines**
4. **Before committing**, offer the user two options — see **Workflow**:
   - Run `prismy generate` locally to generate translations immediately, or
   - Commit and push as-is, then generate translations via the Prismy comment on the pull request

## Wording Guidelines

Before editing any locale file or writing user-facing strings, fetch your project's approved terminology and tone of voice. One fetch per locale per session is sufficient — no need to re-fetch unless the user asks.

### Step 1 — Fetch glossary terms

```bash
prismy glossary --language fr-FR
```

Replace `fr-FR` with the appropriate locale. The glossary contains approved terms that must be used consistently. Always use these exact terms — do not substitute synonyms or alternatives.

### Step 2 — Fetch AI instructions

```bash
prismy ai-instructions
```

This returns:

- **Product context** — what the product does and who it is for; keep this in mind when writing any copy
- **Wording rules** — explicit rules about tone, style, and phrasing; follow these strictly

## Workflow

When adding or modifying user-facing strings:

1. If `prismy.json` exists, check `mainLanguage` and `filesToSync` for context
2. Fetch glossary terms and AI instructions (see **Wording Guidelines** above)
3. Add/modify keys in source locale files only
4. Run `prismy generate` to create translations for all target languages
5. Commit all updated files together
6. After the branch is pushed, share the Prismy link with the product or business team so they can review and adjust the wording:
   `https://app.prismy.io/translations?branch=[branch]&repo=[repo]`

## Configuration

If `prismy.json` exists at the project root, read it to understand:

- `mainLanguage`: The source language (only edit these files)
- `mainBranch`: The branch to compare against
- `filesToSync`: Where locale files live and their format

## Installation

If `prismy` is not installed, run:

```bash
npm install -g prismy-cli
```

## Troubleshooting

If `prismy generate` fails, check the error message. For authentication issues, ask the user to set up their API key — see <https://docs.prismy.io/tech/cli> for details.

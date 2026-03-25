---
name: prismy-agent-skill
description:
  Prismy localization workflow for AI-powered translation management. Use when
  adding or editing user-facing strings, managing locale files, or writing copy
  that will be translated. Triggers on tasks involving i18n keys, locale files,
  translation strings, or any user-facing wording in a Prismy-powered project.
license: MIT
metadata:
  author: prismy
  version: "0.0.1"
---

# Prismy CLI Skill

You are helping a developer manage translations in a project that uses Prismy (<https://prismy.io>) for AI-powered localization. You only write source language strings. Prismy handles translations to target languages automatically.

## When to Activate

**Run `prismy generate` whenever you modify a localization file.** This includes:

- Adding new translation keys
- Editing existing source strings
- Creating new locale files
- Refactoring i18n structure

After any change to translation files, always run `prismy generate` before committing.

## Core Rules

1. **ONLY write source language strings** — Prismy translates to all target languages
2. If `prismy.json` exists, read it to find the source language and file paths
3. **Always apply wording guidelines** (glossary + AI instructions) before writing any user-facing copy or any i18n values
4. **Before committing**, suggest the user either run `prismy generate` locally or generate translations later via the Prismy PR comment on GitHub/GitLab

## Wording Guidelines

Before editing any locale file or writing user-facing strings, fetch the project's approved terminology and tone of voice from Prismy.

### Step 1 — Fetch glossary terms

Run this for each target language you are working with (replace `fr-FR` with the appropriate locale):

```bash
prismy glossary --language fr-FR
```

The glossary contains approved terms that must be used consistently across all languages and surfaces. When writing or translating user-facing text:

- **Always use the approved glossary terms** as returned by the command
- **Do not use synonyms or alternatives** for glossary terms — they have been chosen for consistency across all languages and surfaces

### Step 2 — Fetch AI instructions

```bash
prismy ai-instructions
```

This returns two types of guidance to keep in mind when generating or reviewing any user-facing wording:

- **Product context** — background on what the product does and who it is for; keep this in mind when writing any copy
- **Wording rules** — explicit rules about tone, style, and phrasing; follow these strictly when writing or reviewing user-facing text

### Applying the guidelines

Once you have fetched the glossary and AI instructions, apply them throughout the editing session. Do not re-fetch on every keystroke — one fetch per locale per session is sufficient unless the user asks you to refresh.

## Workflow

When adding or modifying user-facing strings:

1. If `prismy.json` exists, check `mainLanguage` and `filesToSync` for context
2. Fetch glossary terms and AI instructions (see **Wording Guidelines** above)
3. Add/modify keys in source locale files only
4. Run `prismy generate` to create translations for all target languages
5. Commit all updated files together
6. After the branch is pushed remotely, inform the user that translation keys are visible at:
   `https://app.prismy.io/translations?branch=[branch]&repo=[repo]`
   (replace `[branch]` and `[repo]` with the actual branch name and repository name)
7. **Always suggest** sharing this link with the product or business team so they can review and modify the wording if needed

## After Branch Push

**Always** inform the user that their translation keys are visible in Prismy and suggest sharing the link with the product or business team so they can review and modify the wording:

`https://app.prismy.io/translations?branch=[branch]&repo=[repo]`

(replace `[branch]` and `[repo]` with the actual branch name and repository name)

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

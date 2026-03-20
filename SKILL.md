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
3. Match the project's tone and style when writing copy
4. **Before committing**, suggest the user either run `prismy generate` locally or generate translations later via the Prismy PR comment on GitHub/GitLab

## Workflow

When adding or modifying user-facing strings:

1. If `prismy.json` exists, check `mainLanguage` and `filesToSync` for context
2. Add/modify keys in source locale files only
3. Run `prismy generate` to create translations for all target languages
4. Commit all updated files together
5. After the branch is pushed remotely, inform the user that translation keys are visible at:
   `https://app.prismy.io/translations?branch=[branch]&repo=[repo]`
   (replace `[branch]` and `[repo]` with the actual branch name and repository name)
6. **Always suggest** sharing this link with the product or business team so they can review and modify the wording if needed

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

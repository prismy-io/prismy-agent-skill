# Prismy Agent Skill

An agent skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code/skills), [Cursor](https://cursor.com/docs/context/skills), [GitHub Copilot](https://github.com/features/copilot), and similar AI coding assistants. Helps work with i18n strings in projects that use Prismy for AI-powered localization.

Your assistant learns to:

- Run `prismy generate` whenever localization files are modified
- Only write source language strings (Prismy handles translations)
- Follow your project's key naming conventions
- Read `prismy.json` for configuration context (if present)

## Install

```bash
npx skills add prismy-io/agent-skill
```

## Prerequisites

The [Prismy CLI](https://www.npmjs.com/package/prismy-cli) must be installed and authenticated:

```bash
npm install -g prismy-cli
prismy auth <your-api-key>
```

Get your API key from [Prismy Settings](https://app.prismy.io/settings).

## How it works

When you modify localization files, your AI assistant will automatically run `prismy generate` to create translations for all target languages. The CLI compares your branch against main to detect new or changed keys.

## More info

- [Prismy](https://prismy.io)
- [Documentation](https://docs.prismy.io)
- [CLI Reference](https://docs.prismy.io/tech/cli)

## License

MIT

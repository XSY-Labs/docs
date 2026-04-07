# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

This is a Mintlify documentation site. Pages are MDX files with YAML frontmatter. Site configuration (navigation, theme, colors, logos) lives in `docs.json`.

## Commands

- `mint dev` — local preview at http://localhost:3000 (auto-reloads on file changes)
- `mint dev --port 3333` — run on a custom port
- `mint broken-links` — validate all internal links
- `mint update` — update CLI to latest version

**Prerequisites:** Node.js v19+, install CLI with `npm i -g mint`

## Architecture

- `docs.json` — central config: navigation tabs/groups, theme, colors, logos, navbar, footer
- `*.mdx` / `**/*.mdx` — documentation pages (MDX = Markdown + JSX components)
- `snippets/` — reusable content fragments, included via `<Snippet file="snippet-intro.mdx" />`
- `api-reference/openapi.json` — OpenAPI 3.1 spec, drives auto-generated API reference pages
- `images/` and `logo/` — static assets
- `.mintignore` — files/dirs excluded from the docs build (like `.gitignore` for Mintlify)

Navigation structure is defined in `docs.json` under `navigation.tabs[].groups[].pages[]`. Page identifiers are file paths without extensions (e.g., `"essentials/markdown"`).

## Content conventions

- Use active voice and second person ("you")
- Sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references
- One idea per sentence

## Adding pages

1. Create an `.mdx` file with YAML frontmatter (`title`, `description`)
2. Add the page path (without extension) to the appropriate group in `docs.json` `navigation`

## Deployment

Pushing to the default branch auto-deploys via the Mintlify GitHub app.

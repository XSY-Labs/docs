---
paths:
  - "**/*.mdx"
  - "docs.json"
---

# Mintlify workflow reminders

Loads when editing MDX pages or `docs.json`. Quick reminders only — the
installed `mintlify:mintlify` skill and the hosted MCP at
`https://mintlify.com/docs/mcp` are the authoritative reference.

## Before writing

- Read `docs.json` to understand the current navigation and theme
- Search for existing pages on the same topic before creating a new one
- Read 2–3 similar pages to match the site's tone and structure

## Frontmatter

Every `.mdx` page requires a `title` field. `description` is strongly
recommended for SEO and the Mintlify search index. Other optional fields:

- `sidebarTitle` — short title used in the sidebar only
- `icon` — Lucide or Font Awesome icon name
- `tag` — small label next to the sidebar title (e.g., "NEW")
- `mode` — page layout (`default`, `wide`, `custom`)
- `keywords` — search and SEO keywords

## Internal links

Use root-relative paths without the file extension. Correct:
`/guides/quickstart`. Wrong: `../guides/quickstart.mdx` or
`https://docs.yieldpoint.io/guides/quickstart`.

## Navigation

New pages must be added to `docs.json` under
`navigation.tabs[].groups[].pages[]`. Pages not listed in navigation are
still URL-addressable as hidden pages, but they won't appear in the
sidebar.

## Before committing

Run both commands and fix any errors:

- `mint broken-links`
- `mint validate`

## Component gotchas

- JSX components need an explicit `import` statement at the top of the page
- Built-in MDX components do not need importing
- Every code block needs a language tag (`bash`, `typescript`, `json`,
  `mdx`, …)
- Every image needs meaningful alt text

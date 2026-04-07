# AGENTS.md

Instructions for AI coding agents working on docs.yieldpoint.io.

## Project overview

This repo is the Mintlify-powered documentation site served at
https://docs.yieldpoint.io. It covers the YieldPoint protocol: user guides,
product overviews, API reference, integration docs, and deployed contract
addresses. The audience is end users of the protocol, integrators building
on UTY/yUTY, and developers consuming the API.

Deployment is fully automated. Push to `main` and the Mintlify GitHub app
publishes the build to the live site.

## Local dev

Prerequisites: Node.js 19+ and the Mintlify CLI (`npm i -g mint`).

- `mint dev` — local preview at http://localhost:3000, auto-reloads on
  file changes
- `mint dev --port 3333` — run on a custom port
- `mint validate` — strict build validation (fails on any warning or error)
- `mint broken-links` — check every internal link
- `mint a11y` — accessibility audit of all content

The `docs/` directory is excluded from the Mintlify build (see `.mintignore`),
so planning artifacts like brainstorms and implementation plans stay out of
the published site.

## Architecture

- `docs.json` — single source of truth for site config: theme, colors, logos,
  navigation, navbar, footer, contextual AI menu options
- `**/*.mdx` — documentation pages. Each page requires YAML frontmatter
  with at least a `title` field
- `snippets/` — reusable content fragments, imported into pages as JSX
  components (currently absent; returns with real snippets)
- `api-reference/openapi.json` — OpenAPI 3.1 spec. Mintlify auto-generates
  endpoint pages from the spec (currently absent; real spec pulls from
  https://api.yieldpoint.io/docs/json)
- `logo/` and root `favicon.svg` — static brand assets
- `.mintignore` — files and directories excluded from the build

Navigation is defined in `docs.json` under
`navigation.tabs[].groups[].pages[]`. Page identifiers are file paths
without the `.mdx` extension, e.g. `"guides/quickstart"`.

## Cross-repo map

| Resource | Path or URL | Purpose |
|---|---|---|
| Smart contracts | `~/dev/yieldpoint/yieldpoint-contracts/` | Foundry project. Deployed addresses in `script/lib/ChainConfig.sol`. Ops scripts in `script/ops/`. Latest audit at `audit/report-cantina-yieldpoint-2026-04-06.pdf` |
| dApp (Nuxt SPA) | `~/dev/yieldpoint/app.yieldpoint.io/` | Live at https://app.yieldpoint.io — deposit/redeem/withdraw/claim/bridge UI. Source for user-facing terminology |
| API (Nest.js) | `~/dev/yieldpoint/api.yieldpoint.io/` | Live at https://api.yieldpoint.io — OpenAPI spec at https://api.yieldpoint.io/docs/json |
| Mintlify plugin | `~/.claude/plugins/marketplaces/mintlify-marketplace/skills/mintlify/` | Installed `mintlify:mintlify` skill — primary source of Mintlify knowledge. Local-scope enablement via `.claude/settings.local.json` |
| Mintlify source clone | `~/dev/tmp/mintlify/` | Upstream Mintlify docs/components/themes. Fallback for inspecting component source |
| Marketing site | https://yieldpoint.io | Product positioning. Do not copy marketing tone into docs |
| Blog / news | https://paragraph.com/@yieldpoint | News and changelog — lives there, not here |
| X / Twitter | https://x.com/xsy_fi | Announcements |
| Discord | https://discord.gg/fdxe4efA2M | Community support |
| Docs site (this repo) | https://docs.yieldpoint.io | What we're editing |

Paths above are absolute to this machine and are not portable across
contributors. A new contributor would need to update this section before
using the memory system.

## External references

Quick-scan list of live URLs referenced throughout this repo:

- Docs site: https://docs.yieldpoint.io
- dApp: https://app.yieldpoint.io
- API: https://api.yieldpoint.io
- OpenAPI spec (JSON): https://api.yieldpoint.io/docs/json
- Marketing: https://yieldpoint.io
- Blog / news: https://paragraph.com/@yieldpoint
- Discord: https://discord.gg/fdxe4efA2M
- X / Twitter: https://x.com/xsy_fi

## Terminology

A minimal vocabulary so prose uses the right nouns consistently. For
anything deeper — mechanics, storage, fee math, security findings — delegate
to the local `yieldpoint` agent at `.claude/agents/yieldpoint.md` rather
than writing from this list.

- **UTY** — Unity. USDC-backed stablecoin, pegged 1:1, Base-only mint/redeem
- **yUTY** — Staked Unity. Yield vault backed by UTY, 7-day unbonding,
  cross-chain
- **Hub chain** — Base. All vault state lives here
- **Spoke chain** — Avalanche and Katana. Users hold tokens and trigger
  cross-chain flows from spokes
- **Composer** — LayerZero V2 component that handles cross-chain message
  composition
- **Bonding period** — Time between a withdrawal request and the claim.
  For yUTY, 7 days

## Content conventions

The `mintlify:mintlify` skill is authoritative for Mintlify writing
standards. The list below is a short summary so authors don't need to load
the full skill every turn.

- Second person, active voice ("you can configure…", not "users can
  configure…" and not "it is possible to…")
- Sentence case for headings and code block titles
- Bold for UI element names ("click **Settings**"), code format for paths,
  commands, and file names (`` `docs.json` ``, `` `mint dev` ``)
- One idea per sentence. Short is better than clever
- Every code block needs a language tag (`bash`, `typescript`, `json`, …)
- Every image needs descriptive alt text
- Cut marketing adjectives ("powerful", "seamless", "robust") — they don't
  help readers
- Cut filler ("it is important to note", "in order to") — say what you mean
- Explain what a thing is before explaining how to use it

## Content boundaries

**In scope:**

- User guides (deposit, redeem, withdraw, claim, bridge)
- Product overviews (UTY, yUTY)
- API reference pages, auto-generated from the OpenAPI spec once wired in
- Deployed contract addresses per chain — reference `ChainConfig.sol` as
  the source of truth rather than duplicating its content
- A Security & audits page that links to the latest audit report at
  `~/dev/yieldpoint/yieldpoint-contracts/audit/report-cantina-yieldpoint-2026-04-06.pdf`
- Integration and developer guides, adapted from the contracts repo when
  relevant. Delegate to the `yieldpoint` agent for mechanism details
- Chain config and cross-chain mechanics at the level an integrator needs

**Out of scope:**

- Blog, news, changelog — these live on https://paragraph.com/@yieldpoint
- Marketing copy — lives on https://yieldpoint.io, do not duplicate
- Yield math and APY derivations — state target APY, not formulas
- Governance token — no timeline, no name (post-XSY rebrand); omit entirely
- Operational runbooks — key rotation, pause procedures, incident response
- Internal admin flows
- Non-public security findings — the XSYL-* findings in the `yieldpoint`
  agent file are not public

**Deferred, revisit later:**

- Governance and roadmap pages (tied to the token-naming decision)
- Partner / B2B gated documentation (separate surface if it ever exists)

## Adding a page

1. Create an `.mdx` file with YAML frontmatter (`title` required,
   `description` strongly recommended)
2. Add the page path without the `.mdx` extension to the appropriate group
   in `docs.json` under `navigation.tabs[].groups[].pages[]`
3. Run `mint broken-links` and `mint validate` before committing

## Deployment

Push to `main`. The Mintlify GitHub app publishes the build to
https://docs.yieldpoint.io automatically. There is no manual deploy step.

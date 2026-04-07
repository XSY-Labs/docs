# YieldPoint docs: delegation and external-tool rules

Always loaded. When to delegate, which skills and MCPs to use, and in
what order.

## When to delegate to the `yieldpoint` agent

Delegate to `.claude/agents/yieldpoint.md` for any question about the
YieldPoint protocol itself. Triggers:

- Smart contract code, architecture, or inheritance
- Cross-chain flows (LayerZero V2, OFT, Composer, `lzCompose`)
- UTY / yUTY mechanics (decimals, bonding, fee sweep, donations)
- Fee economics and revenue math
- Security findings (XSYL-* series from the Cantina audit)
- Deployed addresses, `ChainConfig.sol`, ops scripts

Example prompts that should trigger delegation:

- "How does a yUTY cross-chain deposit work?"
- "What contracts are deployed on Avalanche?"
- "What was XSYL-2 and how was it fixed?"

Do not answer these from training data.

## When to use the `mintlify:mintlify` skill and hosted MCP

For any Mintlify feature question — components, `docs.json` fields,
navigation, themes, deploy behavior — use the installed `mintlify:mintlify`
skill and the hosted MCP at `https://mintlify.com/docs/mcp`. These are
more current than training data.

## When to use context7

Use context7 for version-pinned external library docs before falling back
to web search. Tool chain:

1. `mcp__claude_ai_Context7__resolve-library-id`
2. `mcp__claude_ai_Context7__query-docs`

Candidate libraries (reach for context7 when a task touches them):

- Mintlify (fallback if hosted MCP is unavailable)
- LayerZero V2 (OFT, OApp, Composer, endpoint IDs)
- Nuxt 3 (for dApp cross-references)
- Viem and Wagmi (contract reads/writes, wallet connectors)
- OpenAPI 3.1 (spec syntax, `$ref`, Mintlify extensions)
- ERC-7540 and ERC-4626 (async vault interfaces)

Do not hardcode library IDs — the context7 catalog drifts.

## External tool priority order

1. Files in this repo (always first; verify before claiming)
2. `mintlify:mintlify` skill and hosted MCP (Mintlify questions)
3. `yieldpoint` agent (protocol questions)
4. context7 (external library docs)
5. WebFetch (live URLs like the API spec or marketing pages)
6. WebSearch (last resort)

## Live resource URLs

- Docs site: https://docs.yieldpoint.io
- dApp: https://app.yieldpoint.io
- API / OpenAPI spec: https://api.yieldpoint.io/docs/json
- Marketing: https://yieldpoint.io
- Blog: https://paragraph.com/@yieldpoint
- Discord: https://discord.gg/fdxe4efA2M
- X / Twitter: https://x.com/xsy_fi

<!-- TODO: Create .claude/rules/api-reference.md when api-reference/ returns.
Plan 001 deletes the directory, so a path-scoped rule would be dead code
until the real OpenAPI spec lands. When it does, create the rule with
paths: ["api-reference/**"] and cover: OpenAPI spec as source of truth,
upstream at https://api.yieldpoint.io/docs/json, reference endpoints as
`GET /endpoint`, manual pages only for workflows the spec can't express. -->

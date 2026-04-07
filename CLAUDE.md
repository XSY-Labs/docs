@AGENTS.md

## Claude Code

- **Mintlify questions:** Prefer the `mintlify:mintlify` skill and the hosted MCP at `https://mintlify.com/docs/mcp` over web search or training data. The skill is the canonical source for components, `docs.json` fields, navigation, and deploy behavior.
- **Protocol / contracts / cross-chain questions:** Delegate to the `yieldpoint` agent at `.claude/agents/yieldpoint.md`. Do not answer from training data. This includes UTY/yUTY mechanics, LayerZero flows, contract inventory, fee economics, and security findings.
- **External library docs:** Use `mcp__claude_ai_Context7__resolve-library-id` then `mcp__claude_ai_Context7__query-docs` before falling back to `WebSearch`. See `.claude/rules/yieldpoint-context.md` for the candidate library list.

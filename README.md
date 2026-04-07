# docs.yieldpoint.io

Mintlify source for [docs.yieldpoint.io](https://docs.yieldpoint.io) — documentation for the YieldPoint protocol.

## Development

```bash
pnpm dev           # local preview at http://localhost:3000
pnpm check         # validate build + broken links + a11y
pnpm check:links   # internal link check only
pnpm check:a11y    # accessibility audit only
```

Prerequisites: Node.js 19+ and `pnpm`. The `mint` CLI is a devDependency resolved via `pnpm install`.

## Deployment

Push to `main`. The Mintlify GitHub app publishes the build to
[docs.yieldpoint.io](https://docs.yieldpoint.io) automatically.

## Contributing

See [`AGENTS.md`](./AGENTS.md) for project conventions, scope boundaries, and
contributor instructions (AI and human).

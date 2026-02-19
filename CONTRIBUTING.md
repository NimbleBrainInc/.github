# Contributing to NimbleBrain

## Prerequisites

- Python 3.13+
- [uv](https://docs.astral.sh/uv/) (package manager)
- [ruff](https://docs.astral.sh/ruff/) (linter/formatter)
- [ty](https://docs.astral.sh/ty/) (type checker)
- Docker (for testing bundles)
- [gh](https://cli.github.com/) (GitHub CLI)
- [Claude Code](https://claude.ai/claude-code)
- mpak CLI (`npm install -g @nimblebrain/mpak`)

Don't worry about installing all of these manually. The onboarding skill checks your environment and tells you what's missing.

## The Workflow

### 1. Pick an integration

Check [open issues](https://github.com/NimbleBrainInc/.github/issues) for available work, or propose your own.

### 2. Create your server repo

```bash
gh repo create NimbleBrainInc/mcp-<name> \
  --template NimbleBrainInc/mcp-server-template --public --clone
cd mcp-<name>
```

### 3. Build with Claude Code

```bash
claude
> /build-mcpb
```

The skill scaffolds the server, walks you through implementing tools, validates the bundle, and authors companion skills.

### 4. Submit a PR

PRs include both server code and companion skills. CI must pass before review.

## Technical Requirements

### MCP Servers (Python)

- Use module execution in manifest: `"args": ["-m", "package_name.server"]`
- Server entry: `if __name__ == "__main__": mcp.run()`
- Stdout must be clean JSON-RPC only. Logs go to stderr.
- 5+ tools covering core operations (list, get, create, update, search)
- Tests with pytest, linting with ruff, type checking with ty

### Auth Patterns

| Auth Type | Complexity | Examples |
|-----------|-----------|----------|
| API key | Low | Notion, Linear, Finnhub, Airtable |
| API key pair | Low | Twilio (SID + token) |
| Private app token | Low | HubSpot |
| OAuth2 | High | Google Workspace |

Start with API key auth. OAuth2 servers should be attempted after you've shipped a simpler server.

### Companion Skills (2-3 per server)

- `SKILL.md` with complete frontmatter and metadata
- Proper tags, category, triggers, examples
- `mpak skill validate` passes
- References MCP server dependency
- At least 2 usage examples

## Definition of Done

### Server
- [ ] 5+ tools implemented
- [ ] `manifest.json` valid (v0.4)
- [ ] Makefile with build/test/clean targets
- [ ] README with install, config, tools reference
- [ ] Tests passing
- [ ] CI passing (lint, format, typecheck, test, bundle, scan)
- [ ] Scanner passes (no critical/high findings)

### Skills
- [ ] 2-3 companion skills authored
- [ ] `mpak skill validate` passes for each
- [ ] `mpak skill pack` succeeds

## Publishing

Publishing happens via GitHub Actions when you create a release tag:

1. Merge your PR to `main`
2. Create a release tag: `git tag v0.1.0 && git push --tags`
3. GitHub Actions builds the bundle, runs the scanner, and publishes to mpak

## Versioning

- All servers start at `v0.x.y` (pre-1.0)
- Forked servers use the `-mcpb.N` suffix
- Bump minor for new tools, patch for fixes

## Communication

- [Discord](https://nimblebrain.ai/discord) for questions and discussion
- File issues on [.github](https://github.com/NimbleBrainInc/.github/issues) for cross-cutting work
- Server-specific issues go on the server's repo

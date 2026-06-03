# bsky-mcp-server

TypeScript/Node MCP server for Bluesky using the AT Protocol SDK (`@atproto/api`). Supports posting, reading feeds, searching, DID resolution, and exposes MCP resources and prompts.

## What it does

Full Bluesky client surface as MCP tools. Handles ATP agent init, post/thread formatting optimized for LLM context, and input validation/URI manipulation via shared utilities.

## Structure

```
src/
  index.ts              Server entry point — McpServer, ATP agent init, tool registrations
  utils.ts              Shared helpers: handle cleaning, URI validation,
                        URL→AT URI conversion, XML escaping
  llm-preprocessor.ts   Post/thread formatting optimized for LLM context windows
  resources.ts          MCP resource registrations (e.g. user profile as a resource)
  prompts.ts            MCP prompt registrations
  scripts/              Utility scripts
test/                   Tests
package.json
tsconfig.json
```

## Configuration

Loaded via dotenv from `.env` then `.env.local`:

| Env var                | Purpose                                          |
|------------------------|--------------------------------------------------|
| `BLUESKY_IDENTIFIER`   | Handle or DID (required)                         |
| `BLUESKY_APP_PASSWORD` | App password (required)                          |
| `BLUESKY_SERVICE_URL`  | AT Protocol PDS URL (default: `https://bsky.social`) |

## Key architecture decisions

- **Lazy ATP agent init** — `initializeBlueskyConnection()` is called at startup. Each tool checks `if (!agent)` and returns a clear error rather than crashing. This keeps the server healthy if credentials are missing or the PDS is temporarily unreachable.
- **`llm-preprocessor.ts` for display** — `formatPostThread()` produces a compact thread representation sized for LLM context windows. Prefer it over passing raw API responses to agents.
- **`utils.ts` is the canonical validation layer** — handle cleaning, URI parsing, and URL→AT URI conversion all live here. Do not duplicate this logic in tool handlers.

## Build

```bash
pnpm install && pnpm build
```

Check `package.json` for test scripts.

## Git workflow

Branch before editing — do not commit directly to `main`.

# Changelog

## [1.1.0] — 2026-02-28

### Added

- `delete-repost` — Remove a repost by its URI

## [1.0.0] — 2026-02-28

### Added

- Initial release of `bsky-mcp-server` — TypeScript MCP server for Bluesky via the AT Protocol SDK
- Fork of the upstream Bluesky MCP server with additional tools and an LLM-optimised post formatter
- Core read tools: `get-timeline-posts`, `get-user-posts`, `get-feed-posts`, `get-list-posts`,
  `get-post-thread`, `get-notifications`, `get-follows`, `get-followers`, `get-liked-posts`,
  `get-reposts`, `get-quotes`, `get-blocks`, `get-mutes`, `get-trends`
- Core write tools: `create-post`, `repost`, `delete-post`, `like-post`, `unlike`,
  `follow-user`, `unfollow`
- `llm-preprocessor.ts` — compact thread/post formatting optimised for LLM context windows
- MCP resources: Bluesky profile descriptor
- MCP prompts: curated prompt templates for common Bluesky workflows
- `utils.ts` — shared helpers: handle cleaning, URI validation, URL→AT URI conversion,
  reply threading fix (root ref), XML escaping
- ATP session management: `BLUESKY_IDENTIFIER`, `BLUESKY_APP_PASSWORD`, `BLUESKY_SERVICE_URL`
- Hours-based pagination for timeline and feed tools

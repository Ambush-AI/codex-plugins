# Release notes

## 0.2.0 — event-driven workflows

- Configures prompt-based or structured post-processing for every future accepted stream event.
- Discovers preconfigured Slack, webhook, and iMessage destinations without exposing credentials.
- Routes streams to delivery channels through the native Ambush event pipeline instead of scheduled polling.
- Mutes and unmutes individual stream-to-channel routes while accurately warning that muting permanently cancels pending work.
- Guides trade-analysis workflows to allow an explicit no-trade result and avoid unsupported certainty.

## 0.1.0 — initial package

- Connects Codex to the production Ambush Streams MCP server with OAuth.
- Creates streams from plain-language monitoring requests.
- Lists streams and inspects stream details and emitted news items.
- Updates stream names and prompts.
- Pauses and resumes streams through status updates.
- Permanently deletes a stream only after explicit confirmation.

Publication status: not submitted.

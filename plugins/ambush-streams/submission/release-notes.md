# Release notes

## 0.2.1 — current API compatibility

- Requires a monitoring prompt when creating a stream and no longer sends the removed base-stream field.
- Recognizes configured Telegram destinations alongside Slack, webhook, and iMessage destinations.
- Keeps the nine-tool event processing, delivery routing, lifecycle, and emission workflow from 0.2.0.

## 0.2.0 — event-driven workflows

- Configures prompt-based or structured post-processing for every future accepted stream event.
- Discovers preconfigured Slack, webhook, and iMessage destinations without exposing credentials.
- Routes streams to delivery channels through the native Ambush event pipeline instead of scheduled polling.
- Mutes and unmutes individual stream-to-channel routes without pausing the stream or deleting the destination.
- Guides trade-analysis workflows to allow an explicit no-trade result and avoid unsupported certainty.

## 0.1.0 — initial package

- Connects Codex to the production Ambush Streams MCP server with OAuth.
- Creates streams from plain-language monitoring requests.
- Lists streams and inspects stream details and emitted news items.
- Updates stream names and prompts.
- Pauses and resumes streams through status updates.
- Permanently deletes a stream only after explicit confirmation.

Publication status: not submitted.

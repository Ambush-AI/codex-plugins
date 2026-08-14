# Ambush Streams for Codex

Ambush Streams lets a consumer create, process, deliver, and manage personalized news streams from Codex. The plugin combines the production OAuth MCP server with workflow guidance for reliable stream discovery, event-time transformation, destination routing, updates, pause and resume, deletion, and emission review.

## Consumer experience

After installing and authenticating once, a consumer can ask in ordinary language:

- "Create a stream for material cybersecurity incidents affecting Canadian banks."
- "Pause my AI regulation stream."
- "For every event from my AI chip stream, produce a cautious trade idea or no-trade result and send it to my connected Trade Ideas channel."
- "What did my semiconductor supply-chain stream emit this week?"

The assistant resolves the appropriate stream and tool arguments. Consumers do not configure an API URL, copy tokens, or need to know that pause and resume are implemented through an update request.

## Package contents

- .mcp.json connects Codex to https://api.ambush.ai/mcp with OAuth.
- skills/manage-ambush-streams teaches stream management, event processing, safe destination routing, irreversible route-muting behavior, and deletion safeguards.
- .codex-plugin/plugin.json contains Codex presentation and package metadata.
- submission contains listing copy, review cases, release notes, and the pre-submission checklist.

## Compatibility

The production MCP API retains legacy identifiers such as list_feeds, create_feed, update_feed, delete_feed, and base_feed_id. Those names are part of the wire contract. The plugin and skill consistently call the user-facing resources streams.

## Status

Version 0.2.0 is prepared for repository-based testing. It has not been submitted to OpenAI's public plugin directory.

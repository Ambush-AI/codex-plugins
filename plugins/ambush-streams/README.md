# Ambush Streams for Codex

Ambush Streams lets a consumer create and manage personalized news streams from Codex. The plugin combines the production OAuth MCP server with workflow guidance for reliable stream discovery, creation, updates, per-event post-processing, delivery routing, pause and resume, deletion, and emission review.

## Consumer experience

After installing and authenticating once, a consumer can ask in ordinary language:

- "Create a stream for material cybersecurity incidents affecting Canadian banks."
- "Pause my AI regulation stream."
- "What did my semiconductor supply-chain stream emit this week?"
- "For every event from that stream, produce a trade thesis or no-trade result and send it to my Trade Ideas Slack channel."

The assistant resolves the appropriate stream, event transformation, and preconfigured destination. Consumers do not configure an API URL, copy tokens or destination credentials into chat, create polling tasks, or need to know that pause and resume are implemented through an update request.

## Package contents

- .mcp.json connects Codex to https://api.ambush.ai/mcp with OAuth.
- skills/manage-ambush-streams teaches stream management, event processing, delivery routing, and deletion safeguards.
- .codex-plugin/plugin.json contains Codex presentation and package metadata.
- submission contains listing copy, review cases, release notes, and the pre-submission checklist.

## Compatibility

The production MCP API retains legacy identifiers such as list_feeds, create_feed, update_feed, delete_feed, and base_feed_id. Those names are part of the wire contract. The plugin and skill consistently call the user-facing resources streams.

## Status

Version 0.2.0 is prepared for repository-based testing. It has not been submitted to OpenAI's public plugin directory.

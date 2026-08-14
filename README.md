# Ambush AI plugins for Codex

This repository is the official Codex marketplace for Ambush AI. It currently publishes the Ambush Streams plugin, which connects Codex to the production Ambush MCP server and teaches Codex how to manage, process, and deliver personalized news streams safely.

This repository is intentionally separate from the other Ambush distribution formats:

- [ambush-stream-skills](https://github.com/Ambush-AI/ambush-stream-skills) is the skills.sh package.
- [claude-plugins](https://github.com/Ambush-AI/claude-plugins) is the Claude Code plugin marketplace.
- This repository is the Codex plugin marketplace.

## Install

Add the marketplace:

~~~sh
codex plugin marketplace add Ambush-AI/codex-plugins --ref main
~~~

Install Ambush Streams:

~~~sh
codex plugin add ambush-streams@ambush-ai
~~~

Restart Codex if it is already open. When prompted, connect your Ambush account through OAuth. You can then ask Codex to create, list, update, process, route, mute, pause, resume, or permanently delete a stream, or review its emitted news items.

## Repository layout

~~~text
.agents/plugins/marketplace.json
plugins/
  ambush-streams/
    .codex-plugin/plugin.json
    .mcp.json
    assets/
    skills/
    submission/
~~~

The marketplace and plugin use Ambush Streams everywhere consumers see the product name. The production MCP API still exposes legacy tool identifiers such as list_feeds and create_feed; the bundled skill maps those identifiers to stream terminology.

## Development

Validate the plugin package with Codex's plugin-creator validator:

~~~sh
python3 /path/to/plugin-creator/scripts/validate_plugin.py plugins/ambush-streams
~~~

Test this checkout as a local marketplace:

~~~sh
codex plugin marketplace add /absolute/path/to/codex-plugins
codex plugin add ambush-streams@ambush-ai
~~~

Remove the local test installation with:

~~~sh
codex plugin remove ambush-streams@ambush-ai
codex plugin marketplace remove ambush-ai
~~~

## Publication status

The repository package is ready for local and team testing. Ambush Streams has not been submitted to OpenAI's public plugin directory. The remaining portal and reviewer steps are tracked in [plugins/ambush-streams/submission/README.md](plugins/ambush-streams/submission/README.md).

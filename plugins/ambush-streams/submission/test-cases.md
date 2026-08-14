# Plugin review cases

Run exactly these six positive and three negative cases with the dedicated reviewer account. Reset the account to the fixture baseline before every case so no case depends on a mutation performed by another case. Record observed tool calls and outcomes without committing credentials or account identifiers.

## Required fixture baseline

Seed and verify these test-only fixtures immediately before submission. Do not wait for live ingestion to produce them, and do not use the stream created in positive case 2 as the input to positive case 4.

| Fixture | Required state | Used by |
| --- | --- | --- |
| `AI regulation` | One uniquely named paused stream whose prompt monitors proposed AI rules broadly. | Positive cases 1 and 3 |
| `AI Chip Supply` | One uniquely named paused stream with exactly the five deterministic emissions below, preventing live ingestion from changing the fixture during review. | Positive cases 4 and 5 |
| `Review Disposable` | One uniquely named active stream. Record its real ID as `<disposable-stream-id>` for the run. | Positive case 6 |
| `General Market Monitor` | One uniquely named active stream, ensuring the list case contains active and paused states. | Positive case 1 |
| `Trade Ideas` | One Slack delivery channel with install status `connected` and destination status `active` that is not initially routed to `AI Chip Supply`. | Positive case 5 |

Seed exactly these five emissions on `AI Chip Supply`, ordered newest first:

1. `2026-01-05T12:00:00Z` — `Review fixture — advanced packaging plant interruption`
2. `2026-01-04T12:00:00Z` — `Review fixture — HBM production allocation change`
3. `2026-01-03T12:00:00Z` — `Review fixture — accelerator export restriction enacted`
4. `2026-01-02T12:00:00Z` — `Review fixture — leading-edge foundry outage`
5. `2026-01-01T12:00:00Z` — `Review fixture — substrate supplier capacity reduction`

Before each case, remove any stream created by an earlier run, restore the four named streams to the states above, and confirm `AI Chip Supply` has exactly those five emissions. If fixture reset fails, stop the review run instead of adapting the expected result to stale state.

## Positive cases

### 1. List and summarize streams

Prompt: `List my Ambush streams and tell me which ones are paused.`

Expected: Invoke `list_feeds`, paginate only if needed to answer completely, and summarize returned names or prompt excerpts and statuses. Do not mutate a stream.

### 2. Create a focused stream

Prompt: `Create an Ambush stream named Advanced Packaging Watch that monitors material disruptions to advanced AI chip packaging capacity.`

Expected: Invoke `create_feed` exactly once with the supplied name and a faithful monitoring prompt. Return the stream ID and status.

### 3. Resume and refine through update

Prompt: `Resume my paused AI regulation stream and change it to focus on enacted rules and enforcement actions.`

Expected: Resolve the exact stream with `list_feeds` when its ID is not already known, then invoke `update_feed` with that stream ID, `status: "active"`, and the revised prompt. Do not search for a separate resume operation. If duplicate names exist, ask the user to choose before writing.

### 4. Review recent emissions

Prompt: `Show me the five latest items emitted by my AI Chip Supply stream.`

Expected: Resolve the uniquely named seeded stream, invoke `list_emissions` with a limit of five, and summarize exactly the five newest seeded emissions in returned order. Do not use a stream created in another case, and do not claim there were no items if the request failed.

### 5. Process and deliver every event without polling

Prompt: `For every new event from my AI Chip Supply stream, produce a cautious trade idea or explicitly say no trade, and send it to my Trade Ideas Slack channel every time the stream fires.`

Expected: Resolve `AI Chip Supply`, inspect it with `get_feed`, invoke `update_feed` once with a faithful `post_processing` prompt that permits `no_trade`, invoke `list_channels`, and invoke `route_feed_channel` with the connected `Trade Ideas` Slack channel. Confirm this applies to future accepted events. Do not create or suggest a scheduled polling task, do not change the stream's monitoring prompt, and do not ask for Slack credentials.

### 6. Delete after exact confirmation

Prompt: `Permanently delete stream <disposable-stream-id>. I confirm that exact stream.`

Expected: Substitute the real disposable stream ID, invoke `delete_feed` once for exactly that ID, and report the deletion. Never claim it is recoverable.

## Negative cases

### 1. Unrelated news question

Prompt: `What are the biggest technology stories today?`

Expected: Do not invoke Ambush Streams merely because the request mentions news.

### 2. Software implementation request

Prompt: `Write a TypeScript RSS parser for my project.`

Expected: Do not invoke Ambush Streams. This is a coding request, not stream management.

### 3. Ambiguous destructive request

Prompt: `Clean up my old streams.`

Expected: It is acceptable to invoke `list_feeds` to show candidates, but do not invoke `delete_feed`. Ask which exact stream or streams the user wants permanently deleted and require confirmation.

## Authentication case

Prompt from a signed-out account: `List my Ambush streams.`

Expected: Start the OAuth connection flow or ask the user to authenticate. Never ask the user to paste a bearer token.

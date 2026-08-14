# MCP reviewer materials

Prepare these materials immediately before submission. Do not commit demo credentials, recording access tokens, portal-generated verification tokens, or user data.

## Demo recording

- [ ] Record the production plugin in every product selected in the portal.
- [ ] Show OAuth sign-in, stream discovery, stream creation, event-time post-processing and routing, a status update, emission review, and the explicit confirmation before deletion.
- [ ] Host the recording at a stable reviewer-accessible HTTPS URL.
- [ ] Enter that URL directly in the submission portal.

## Tool annotation justifications

Copy these justifications into the portal for the production tool scan.

| Tool | `readOnlyHint` | `openWorldHint` | `destructiveHint` |
| --- | --- | --- | --- |
| `list_feeds` | `true` — reads stream summaries without changing account state. | `false` — reads only the authenticated user's Ambush data and does not contact arbitrary external systems. | `false` — cannot alter or remove data. |
| `get_feed` | `true` — reads one stream, its channels, usage, and recent emissions without changing state. | `false` — reads only the authenticated user's Ambush data. | `false` — cannot alter or remove data. |
| `list_channels` | `true` — reads delivery destination metadata without changing state; webhook paths and internal metadata are redacted before model exposure. | `false` — reads only the authenticated user's Ambush data. | `false` — cannot alter or remove data. |
| `create_feed` | `false` — creates persistent stream state. | `false` — writes only to the authenticated user's Ambush account and does not act on arbitrary external systems. | `false` — creation does not remove or irreversibly overwrite existing data, and the new stream can be deleted separately. |
| `update_feed` | `false` — changes a stream's name, prompt, active/paused status, or event transformation. | `false` — writes only to the authenticated user's Ambush account. | `false` — supported changes are reversible through another update and do not delete the stream or its history. |
| `route_feed_channel` | `false` — creates or reactivates a stream-to-destination route. | `false` — routes only between resources in the authenticated user's Ambush account. | `false` — the route can be muted without deleting either resource. |
| `update_feed_channel_route` | `false` — mutes or unmutes future deliveries on an existing route. | `false` — updates only the authenticated user's Ambush route. | `true` — muting permanently cancels pending deliveries and attempts, and unmuting does not recreate them. |
| `delete_feed` | `false` — changes account state by deleting a stream. | `false` — affects only the authenticated user's Ambush account. | `true` — permanently removes the selected stream and cannot be undone. |
| `list_emissions` | `true` — reads emission history without changing state. | `false` — reads only the authenticated user's Ambush data. | `false` — cannot alter or remove data. |

The MCP server also supplies explicit `idempotentHint` values. Reconfirm all annotations against the production scan immediately before submission.

## OAuth reviewer account

- [ ] Create a dedicated review-only Ambush account with a verified email address.
- [ ] Ensure sign-in does not require MFA, an emailed code or link, device approval, employee-controlled SSO, CAPTCHA, or manual intervention.
- [ ] Confirm the complete sign-in and OAuth consent flow works without a VPN, allowlist, company network, or other private access.
- [ ] Have someone other than the account creator complete a clean-browser preflight using only the credentials entered in the portal.
- [ ] Reset and seed every named stream and emission fixture in [test-cases.md](test-cases.md).
- [ ] Verify the account has no production customer data and no privileged internal access.
- [ ] Enter credentials only in the portal's protected reviewer-credentials fields.
- [ ] Keep the account active through review, then revoke or rotate it after approval.

## Production tool scan

- [ ] Run the portal's tool scan against `https://api.ambush.ai/mcp` after the final tool metadata is live.
- [ ] Confirm all nine expected tools are present and the scan reports no undeclared UI templates or external frame domains.
- [ ] Confirm every tool has explicit read-only, open-world, and destructive annotations matching the table above.
- [ ] Record the successful scan timestamp in the portal.

## UI and screenshots

The MCP server currently exposes tools without custom UI output templates. Submit screenshots only if the current portal requirements or a future production scan call for them.

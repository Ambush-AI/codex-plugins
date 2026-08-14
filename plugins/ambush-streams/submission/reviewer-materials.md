# MCP reviewer materials

Prepare these materials immediately before submission. Do not commit demo credentials, recording access tokens, portal-generated verification tokens, or user data.

## Demo recording

- [ ] Record the production plugin in every product selected in the portal.
- [ ] Show OAuth sign-in, stream discovery, stream creation, a status update, emission review, and the explicit confirmation before deletion.
- [ ] Host the recording at a stable reviewer-accessible HTTPS URL.
- [ ] Enter that URL directly in the submission portal.

## Tool annotation justifications

Copy these justifications into the portal for the production tool scan.

| Tool | `readOnlyHint` | `openWorldHint` | `destructiveHint` |
| --- | --- | --- | --- |
| `list_feeds` | `true` — reads stream summaries without changing account state. | `false` — reads only the authenticated user's Ambush data. | `false` — cannot alter or remove data. |
| `get_feed` | `true` — reads one stream, its channels, usage, and recent emissions. | `false` — reads only the authenticated user's Ambush data. | `false` — cannot alter or remove data. |
| `create_feed` | `false` — creates persistent stream state. | `false` — writes only to the authenticated user's Ambush account. | `false` — creation does not remove or irreversibly overwrite existing data. |
| `update_feed` | `false` — changes a stream's name, prompt, or status. | `false` — writes only to the authenticated user's Ambush account. | `false` — supported changes are reversible through another update. |
| `delete_feed` | `false` — changes account state by deleting a stream. | `false` — affects only the authenticated user's Ambush account. | `true` — permanently removes the selected stream and cannot be undone. |
| `list_emissions` | `true` — reads emission history without changing state. | `false` — reads only the authenticated user's Ambush data. | `false` — cannot alter or remove data. |

Reconfirm all annotations against the production scan immediately before submission.

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
- [ ] Confirm all six expected tools are present.
- [ ] Confirm every tool has explicit read-only, open-world, and destructive annotations matching the table above.
- [ ] Record the successful scan timestamp in the portal.

## UI and screenshots

The MCP server currently exposes tools without custom UI output templates. Submit screenshots only if the current portal requirements or a future production scan call for them.

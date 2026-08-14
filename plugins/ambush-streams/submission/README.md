# Public-directory submission checklist

Use this directory as the source of truth for a future Ambush Streams submission through the OpenAI Platform plugin portal. The repository package is ready for local and team testing, but it has not been submitted.

## Before submission

- [x] Production MCP uses HTTPS at `https://api.ambush.ai/mcp`.
- [x] OAuth authorization, dynamic client registration, and PKCE work with Codex.
- [x] MCP discovery metadata and protected-resource challenges are public.
- [x] Tool annotations distinguish reads, writes, and destructive deletion.
- [x] A privacy policy is public at `https://reflex.app/privacy`.
- [x] Support is public at `https://reflex.app/support` and `support@ambush.ai`.
- [ ] Publish legal-approved Ambush terms of service at a public HTTPS URL, add `termsOfServiceURL` to the plugin manifest, and replace the pending value in the listing copy.
- [ ] Run every case in [test-cases.md](test-cases.md) against the production plugin build.
- [ ] Complete every external item in [reviewer-materials.md](reviewer-materials.md), including the demo recording, reviewer account, and current portal tool scan.
- [ ] From a clean browser with no existing session, verify the reviewer credentials complete sign-in and OAuth without MFA, verification prompts, manual assistance, or private-network access.
- [ ] Generate the domain-verification token in the submission portal and deploy the challenge response described below.
- [ ] Capture any screenshots requested by the portal from the production consumer flow.
- [ ] Obtain product and legal sign-off for country availability and listing copy.

## Domain verification

The portal-generated verification token must be served from:

~~~text
https://api.ambush.ai/.well-known/openai-apps-challenge
~~~

Do not commit a placeholder token. After the portal generates the real value:

1. Serve the exact value as the only plain-text response body at that URL.
2. Deploy the change to production.
3. Verify the endpoint returns HTTP 200 with the exact token.
4. Complete domain verification in the portal.

## Portal inputs

- Listing copy: [listing.md](listing.md)
- Review cases: [test-cases.md](test-cases.md)
- Reviewer materials: [reviewer-materials.md](reviewer-materials.md)
- Initial release notes: [release-notes.md](release-notes.md)
- MCP endpoint: `https://api.ambush.ai/mcp`
- Authentication: OAuth 2.1-compatible authorization code flow with PKCE and dynamic client registration
- Support URL: `https://reflex.app/support`
- Support email: `support@ambush.ai`

## Publish and verify

Only after every required item above is complete:

1. Submit the plugin in the OpenAI Platform portal and address review feedback in this package.
2. Publish the approved version to the public plugin directory.
3. Install it from clean Codex and ChatGPT accounts, complete OAuth, and run the positive review cases.
4. Confirm unrelated prompts do not invoke the plugin and destructive deletion still requires explicit confirmation.
5. Record the published version and approval date in the release notes.

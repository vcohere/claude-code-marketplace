---
category: Third-Party Integration Misconfig
severity: medium
prevalence: occasional
---

# OAuth/login redirect target is attacker-controllable

Check whether OAuth / social-login and post-authentication redirect handling restricts the redirect target to an allow-list, rather than honoring an attacker-controllable destination.

Where to look:
- Login and callback handling, and any `redirect`, `redirect_to`, `next`, or `returnTo` parameter passed through the auth flow.
- Provider configuration: allowed redirect URIs in Supabase/Firebase/OAuth provider settings.

What to do:
1. Check whether the post-login redirect destination is taken from a user-supplied parameter and, if so, whether it is validated against an allow-list of permitted URLs.
2. Check the provider's configured redirect URIs for wildcard or overly broad entries, including stray localhost entries left in production config.
3. Flag flows that send the user — and potentially the auth code/token — to a destination an attacker can influence.

Report back:
- The redirect handling and provider configuration you checked.
- Any unvalidated redirect parameter or loose redirect-URI configuration — name the exact file/route or config setting.
- For each, one plain sentence on what it would mean in practice — for example, that an attacker could craft a login link that sends the user, or the auth code, to a destination they control.
- If redirect targets are restricted to an allow-list, say so plainly and note what you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file/route or config references.

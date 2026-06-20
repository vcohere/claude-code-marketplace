---
category: Authentication & Session Handling
severity: high
prevalence: occasional
---

# Auth provider configured with a weak identity boundary

Check whether the authentication provider is configured in a way that weakens the identity that the rest of the app relies on.

Where to look:
- Auth provider configuration: Supabase `config.toml` / dashboard auth settings, Firebase Auth settings, or equivalent.
- Settings such as anonymous sign-ins, email auto-confirm, email verification requirements, and sign-up scope.

What to do:
1. Inspect the auth configuration for settings that lower the bar on identity: anonymous sign-ins enabled, email auto-confirm on, no email verification required, or otherwise unrestricted account creation.
2. Identify whether downstream access checks (RLS, ownership checks, role checks) trust the identity produced by this configuration.
3. Flag combinations where a weak or easily spoofed identity is then trusted by protected resources.

Report back:
- The auth settings you checked.
- Any setting that weakens the identity boundary — name the setting and its value, and note a protected resource that trusts the resulting identity.
- For each, one plain sentence on what it would mean in practice — for example, that an attacker could create unlimited or unverified identities that still pass the app's authenticated checks.
- If the auth configuration establishes a verified, non-trivial identity, say so plainly and note the settings you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact setting names and values.

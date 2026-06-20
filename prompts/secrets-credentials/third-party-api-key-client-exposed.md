---
category: Secrets & Credentials
severity: high
prevalence: common
---

# Metered third-party API key called from the browser

Check whether any metered third-party API key that should be server-side is instead called from the browser or embedded in the frontend.

Where to look:
- Client-side components and the built bundle.
- Calls to paid/metered providers: LLM APIs (OpenAI, Anthropic), email/SMS providers, paid data APIs, and similar.
- Build-time public env variables (`NEXT_PUBLIC_*`, `VITE_*`) holding provider keys.

What to do:
1. Search client code for direct calls to billable third-party APIs that include an API key in the request (for example, an `Authorization: Bearer ...` header constructed in frontend code).
2. Check whether keys for billable services are exposed through public env variables and therefore present in the shipped bundle.
3. Distinguish keys that are designed to be public from keys that bill the account's usage; only the latter is a finding.

Report back:
- Where you looked and which providers you checked.
- Any billable provider key reachable from the client — name the exact file and variable, and the provider it bills.
- For each, one plain sentence on what it would mean in practice — for example, that anyone extracting the key from the bundle could make calls that bill the account.
- If no billable third-party key is exposed to the client, say so plainly and note what you inspected.

Do not suggest fixes or assign severity. Report only what you find, with exact file and variable names.

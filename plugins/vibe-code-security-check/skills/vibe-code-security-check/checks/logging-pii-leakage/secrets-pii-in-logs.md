---
category: Logging & PII Leakage
severity: medium
prevalence: common
---

# Secrets or PII written to logs and the console

Check whether logging writes secrets, tokens, or personal data to the browser console or server logs.

Where to look:
- `console.log`/`console.error` calls and server-side logging statements.
- Logs of whole objects: sessions, request bodies, user records, headers, or API responses.

What to do:
1. Find logging statements that print whole objects or sensitive values.
2. Check whether any log includes tokens, API keys, passwords, or PII (emails, phone numbers, full user records) — for example, `console.log(session)`, `console.log(req.body)`, or logging a user object.
3. Distinguish logs shipped to production (browser console or server log sinks) from purely local development-only logging where possible.

Report back:
- The logging statements you checked.
- Any log that writes secrets, tokens, or PII — name the exact file and line, and which sensitive value it prints (name the field, not the value).
- For each, one plain sentence on what it would mean in practice — for example, that the value appears in the browser console or in server logs where it can be read.
- If no logging exposes secrets or PII, say so plainly and note what you checked.

Do not suggest fixes or assign severity. Report only what you find, with exact file and line references.

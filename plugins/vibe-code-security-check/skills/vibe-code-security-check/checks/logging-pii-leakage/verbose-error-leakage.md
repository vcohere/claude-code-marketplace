---
category: Logging & PII Leakage
severity: medium
prevalence: common
---

# Errors return stack traces and DB internals to the client

Check whether server errors return stack traces, raw database errors, or other internal details to the client instead of a generic message.

Where to look:
- API route and serverless error handling.
- Catch blocks and error responses that serialize an error, such as `res.status(500).json({ error: err.message })` or returning `err.stack`.
- Framework default error behavior in production.

What to do:
1. Find where handlers respond on error.
2. Check whether the response body can contain raw error detail: database errors (for example, a Postgres message naming a column), stack traces with file paths, or library/version internals.
3. Flag handlers that return such detail to the client rather than a generic, non-revealing message.

Report back:
- The error paths you checked.
- Any handler that returns raw error detail to the client — name the exact file and route, and what kind of detail leaks (DB error, stack trace, etc.).
- For each, one plain sentence on what it would mean in practice — for example, that the response reveals backend structure such as schema, file paths, or libraries to anyone triggering the error.
- If error responses return only generic messages, say so plainly and list what you checked.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

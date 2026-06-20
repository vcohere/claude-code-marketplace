---
category: API & Backend Surface
severity: high
prevalence: common
---

# Write endpoints reachable with no authentication

Check whether every endpoint that creates, updates, or deletes data requires and validates an authenticated identity before performing the write.

Where to look:
- API routes, serverless/edge functions, and RPC handlers that handle POST, PUT, PATCH, or DELETE.
- Mutation handlers behind forms and buttons, evaluated independently of the UI that calls them.

What to do:
1. Enumerate every handler that writes data (create/update/delete), including ones that look like they are only ever reached from an authenticated screen.
2. For each, check whether the handler itself verifies a session or token at the top before mutating — not whether the page that calls it requires login.
3. Flag any write handler that performs its mutation with no authentication guard, so it could be called directly (for example, via `curl`) by an unauthenticated caller.

Report back:
- The mutation handlers you checked.
- Any write endpoint with no authentication check — name the exact file, route, and HTTP method.
- For each, one plain sentence on what it would mean in practice — for example, that anyone could call the endpoint directly to create, change, or delete records without logging in.
- If every mutation endpoint enforces authentication in the handler itself, say so plainly and list the routes you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

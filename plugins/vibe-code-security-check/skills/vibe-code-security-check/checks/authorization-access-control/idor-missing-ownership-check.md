---
category: Authorization & Access Control
severity: high
prevalence: common
---

# Records fetched by ID with no ownership check (IDOR)

Check whether endpoints that fetch or modify a record by an ID confirm that the record belongs to the authenticated user, not merely that someone is logged in.

Where to look:
- API routes, serverless/edge functions, and RPC handlers (Next.js route handlers, Express routes, Node handlers, Supabase/Firebase functions).
- Any handler that reads an `id`, `slug`, or similar identifier from the URL, query string, or request body and uses it to load or change a record.

What to do:
1. Find every handler that takes a record identifier from the request and fetches or mutates that record.
2. For each, separate two distinct checks: (a) is the caller authenticated, and (b) does the handler verify the record's owner matches the authenticated user (for example, comparing a stored `user_id` against `auth.uid()` or `session.user.id`).
3. Flag any handler that performs (a) but not (b) — it returns or changes the record for any logged-in user regardless of who owns it.
4. Watch specifically for queries that filter only by the request-supplied id and never by the current user's id.

Report back:
- The routes/handlers you checked.
- Any handler that loads or modifies a record by request-supplied id without an ownership check — name the exact file and route.
- For each, one plain sentence on what it would mean in practice — for example, that changing the id in the request would return or alter another user's record.
- If every such handler verifies ownership against the authenticated user, say so plainly and list the routes you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

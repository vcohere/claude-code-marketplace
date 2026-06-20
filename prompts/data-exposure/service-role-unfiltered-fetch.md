---
category: Data Exposure
severity: critical
prevalence: occasional
---

# Admin-client endpoints return data without a per-user filter

Check whether server endpoints that use the service-role / admin database client re-apply a per-user filter on every query against user data.

Where to look:
- Server-side routes, serverless functions, and handlers that initialize a privileged database client (for example, a Supabase client built with the service-role key, or an admin SDK).
- Queries in those handlers that read user-data tables.

What to do:
1. Identify every call site that uses the admin/service-role client, as opposed to the user-scoped client.
2. For each query against a user-data table, check whether the handler adds its own per-user filter (for example, `.eq('user_id', session.user.id)` or an equivalent `where` clause tied to the authenticated user).
3. Flag any privileged-client query that returns user data without such a filter. The service-role client bypasses Row-Level Security entirely, so RLS being enabled does not protect these routes — the filter must be in the handler.
4. Keep this distinct from per-record ownership bugs: here the concern is a query returning the whole table or all users' rows.

Report back:
- The privileged-client call sites you checked.
- Any query that returns user data with no per-user filter — name the exact file, route, and table/query.
- For each, one plain sentence on what it would mean in practice — for example, that calling the endpoint returns every user's rows, not just the caller's.
- If every service-role query against user data is scoped to the requesting user, say so plainly and list the call sites you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

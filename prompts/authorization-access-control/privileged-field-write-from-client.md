---
category: Authorization & Access Control
severity: high
prevalence: occasional
---

# Privileged fields (role, credits, ownership) writable from the client

Check whether users can write fields that should be server-controlled — such as `role`, `is_admin`, `plan`, `credits`, `balance`, or ownership (`user_id`) — through update endpoints or database policies.

Where to look:
- "Update" handlers that persist request data, especially ones that spread the request body into an update (for example, `update({ ...req.body })`).
- Supabase/Postgres RLS update policies and any column-level restrictions.
- Firestore rules governing updates.

What to do:
1. Find write paths where a user can update their own record.
2. Check whether those paths restrict which columns/fields the client may set, or whether arbitrary fields in the request are persisted.
3. For RLS update policies, check whether a policy like `using (auth.uid() = id)` lets the user update their own row but places no restriction on which columns they may change.
4. Flag any path where a request could set a privileged field (for example, `PATCH` with `{ "is_admin": true }` or `{ "credits": 999999 }`).

Report back:
- The write paths and policies you checked.
- Any path that lets the client set a server-controlled field — name the exact file/route or policy, and the privileged field it can reach.
- For each, one plain sentence on what it would mean in practice — for example, that a user could grant themselves admin rights or arbitrary credits through a normal update request.
- If every write path restricts the client to non-privileged fields, say so plainly and list what you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file/route or policy references.

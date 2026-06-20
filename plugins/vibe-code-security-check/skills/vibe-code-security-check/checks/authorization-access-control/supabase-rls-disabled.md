---
category: Authorization & Access Control
severity: critical
prevalence: common
---

# Row-Level Security disabled on user-data tables

Check whether Row-Level Security (RLS) is correctly enforced on every database table that holds user or business data.

Where to look:
- Migration files, `schema.sql`, or the Supabase/Postgres schema definition.
- Any `.sql` files that create tables or define policies.
- If you can query the live database, inspect the `rowsecurity` flag per table and the contents of `pg_policies`.

What to do:
1. Enumerate every table that stores user accounts, user-generated content, orders, messages, payments, or any other per-user or business data.
2. For each table, determine whether RLS is enabled.
3. Where RLS is enabled, read the actual policy definitions rather than trusting the enabled flag. A policy whose condition is `using (true)`, or one with no condition tying a row to the requesting user, does not restrict access even though RLS reports as on.
4. For each policy, identify which role it applies to (`anon`, `authenticated`, etc.) and whether that role can read or write rows it does not own.

Report back:
- The tables you checked.
- Any table with RLS disabled entirely (name the table).
- Any table with RLS enabled but a policy that does not scope access to the owning user (name the table and quote the policy).
- For each issue, one plain sentence on what it would mean in practice — for example, that a visitor holding the public anon key could read or modify every row in that table.
- If every user-data table has RLS enabled with a policy that correctly restricts rows to their owner, say so plainly and list the tables you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact table and policy names.

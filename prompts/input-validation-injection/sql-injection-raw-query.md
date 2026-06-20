---
category: Input Validation & Injection
severity: critical
prevalence: occasional
---

# Raw SQL built with string-interpolated user input

Check whether any raw SQL or database call builds its query by interpolating user input into the query string instead of using parameterized queries.

Where to look:
- Raw query calls (for example, `db.query(...)`, a Postgres client's query method, or a raw-SQL escape hatch in an ORM/SDK).
- RPC or SQL strings that include request-derived values.

What to do:
1. Find places that execute raw SQL or build SQL strings.
2. For each, check whether user/request input is inserted via string interpolation or template literals (for example, a template string putting an email value directly inside `WHERE email = '...'`) rather than passed as a bound parameter.
3. Flag any query where untrusted input is concatenated into the SQL text.

Report back:
- The raw-query sites you checked.
- Any query that interpolates user input into the SQL string — name the exact file and line, and the input involved.
- For each, one plain sentence on what it would mean in practice — for example, that crafted input could alter the query to read or change data beyond what was intended.
- If every dynamic query uses bound parameters, say so plainly and list the sites you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and line references.

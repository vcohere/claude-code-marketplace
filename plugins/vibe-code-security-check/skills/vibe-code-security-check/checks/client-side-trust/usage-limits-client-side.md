---
category: Client-Side Trust
severity: medium
prevalence: common
---

# Free-tier limits enforced only in the browser

Check whether free-tier or usage limits are enforced on the server, or only counted and blocked in the browser.

Where to look:
- Client-side limit logic: counters in component state, `localStorage`/`sessionStorage` usage counts, conditions like `if (uses >= 3)`.
- The endpoint behind the limited action.

What to do:
1. Find where a usage limit or quota is applied.
2. Determine whether the count is tracked and enforced server-side per user, or only in client state.
3. Check the underlying endpoint: does it impose its own per-user count, or will it serve the action regardless of the client-side counter?
4. Flag limits that exist only in the browser and can be bypassed by clearing storage or calling the API directly.

Report back:
- The limited actions you checked.
- Any limit enforced only client-side with an uncapped endpoint behind it — name the exact file/route and the limited action.
- For each, one plain sentence on what it would mean in practice — for example, that a user could reset the browser counter or call the endpoint directly to exceed the limit.
- If usage limits are enforced server-side, say so plainly and note where the enforcement lives.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

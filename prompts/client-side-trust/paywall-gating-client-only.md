---
category: Client-Side Trust
severity: medium
prevalence: common
---

# Premium content gated only in the UI

Check whether plan-gated (premium) content and features are enforced on the server, or only hidden in the user interface while the underlying endpoint serves any authenticated user.

Where to look:
- UI that conditionally renders features based on a client-side flag (for example, `isPro`, `plan === 'premium'`).
- The data endpoints or queries behind those premium features.

What to do:
1. Identify each premium feature and the client-side condition that hides or shows it.
2. For each, locate the endpoint or query that actually returns the premium data or performs the premium action.
3. Check whether that server path verifies the user's entitlement/plan before responding, or whether it returns the data to any logged-in user regardless of plan.
4. Flag features where the only gate is the UI condition.

Report back:
- The premium features and their backing endpoints you checked.
- Any feature whose data path serves the content without a server-side entitlement check — name the exact file and route, and note the UI gate that hides it.
- For each, one plain sentence on what it would mean in practice — for example, that a non-paying authenticated user could request the premium data directly.
- If every premium path enforces entitlement on the server, say so plainly and list what you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

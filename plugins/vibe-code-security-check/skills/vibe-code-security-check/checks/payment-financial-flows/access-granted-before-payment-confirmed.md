---
category: Payment & Financial Flows
severity: high
prevalence: occasional
---

# Paid access unlocked without confirming payment

Check whether paid access is granted only after the server confirms the payment, rather than on a client-side success signal.

Where to look:
- Post-checkout handling: success redirect routes (for example, `/success`), and any endpoint the client calls to "unlock" after checkout.
- The point where entitlement/access is recorded.

What to do:
1. Trace what causes access to be granted.
2. Determine whether it depends on a server-confirmed payment (a verified webhook event or a server-side retrieval of the payment's status) or on the client reaching a success URL / calling an unlock endpoint.
3. Flag any flow where entitlement is set based on client navigation or a user-callable request without server-side payment verification.

Report back:
- The unlock/entitlement paths you checked.
- Any path that grants access without server-side payment confirmation — name the exact file and route.
- For each, one plain sentence on what it would mean in practice — for example, that a user could reach the success URL or call the unlock endpoint to gain paid access without a confirmed charge.
- If access is granted only on server-confirmed payment, say so plainly and note where the confirmation happens.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

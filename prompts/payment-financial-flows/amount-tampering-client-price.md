---
category: Payment & Financial Flows
severity: high
prevalence: occasional
---

# Charge amount taken from the client

Check whether the amount charged at payment is derived on the server from trusted data, rather than accepted from the client request.

Where to look:
- Code that creates a payment intent, checkout session, or charge (for example, Stripe `paymentIntents.create` / `checkout.sessions.create`).
- The path from the frontend "pay" action to the payment provider call.

What to do:
1. Trace where the `amount` (or price/total) passed to the payment provider comes from.
2. Determine whether that value is looked up server-side from a trusted source (such as the product's price in the database, keyed by product id) or read from the request body / client state.
3. Flag any payment call where the charged amount originates from client-controllable input (for example, `amount: req.body.amount`).

Report back:
- The payment-creation code you checked.
- Any case where the charged amount comes from the client rather than a server-side lookup — name the exact file and the line where the amount is set.
- For each, one plain sentence on what it would mean in practice — for example, that a buyer could edit the request to pay an arbitrary amount for a product.
- If the charged amount is always derived server-side from trusted data, say so plainly and note where the lookup happens.

Do not suggest fixes or assign severity. Report only what you find, with exact file and line references.

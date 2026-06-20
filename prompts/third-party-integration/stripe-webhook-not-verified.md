---
category: Third-Party Integration Misconfig
severity: high
prevalence: occasional
---

# Payment webhook accepts unverified events

Check whether payment webhook handlers verify the provider's signature before trusting and acting on the event.

Where to look:
- Webhook route handlers for the payment provider (for example, a Stripe webhook endpoint).
- The point where the handler reads the request body and branches on the event type (such as `checkout.session.completed`).

What to do:
1. Find each payment webhook handler.
2. Check whether it verifies the event signature using the provider's verification method and the signing secret (for Stripe, `stripe.webhooks.constructEvent(rawBody, signature, secret)` against the raw request body) before using the event.
3. Flag any handler that parses the body and acts on the event — for example, marking an order paid or granting access — without verifying the signature first.

Report back:
- The webhook handlers you checked.
- Any handler that acts on events without signature verification — name the exact file and route.
- For each, one plain sentence on what it would mean in practice — for example, that anyone could send a forged "payment succeeded" request to the endpoint and unlock paid functionality without paying.
- If every payment webhook verifies the signature before acting, say so plainly and list the handlers you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

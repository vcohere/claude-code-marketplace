---
category: Abuse & Cost Runaway
severity: medium
prevalence: common
---

# Billable operations with no per-user metering

Check whether endpoints that trigger a billable operation per call have a per-user quota or server-side cap.

Where to look:
- Endpoints that call paid operations: LLM completions, image generation, email/SMS sending, or heavy compute.
- Any per-user counter, credit check, quota, or throttle guarding those calls.

What to do:
1. Identify each endpoint that incurs a real cost per invocation.
2. For each, check whether the server enforces a per-user cap, credit/quota check, or throttle before performing the billable operation.
3. Flag endpoints where the billable call has no usage gate, so a script could invoke it repeatedly. This concerns cost and abuse, distinct from authentication rate-limiting.

Report back:
- The billable endpoints you checked.
- Any that perform the costly operation with no per-user cap or quota — name the exact file and route, and the operation it triggers.
- For each, one plain sentence on what it would mean in practice — for example, that a single actor could call the endpoint in a loop and run up the account's bill.
- If every billable endpoint enforces a server-side usage limit, say so plainly and list what you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

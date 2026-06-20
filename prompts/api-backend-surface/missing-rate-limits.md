---
category: API & Backend Surface
severity: medium
prevalence: common
---

# Sensitive endpoints have no rate limiting

Check whether sensitive, abusable endpoints have server-side rate limiting or lockout.

Where to look:
- Authentication and account endpoints: login, signup, password reset, OTP/verification, magic-link requests.
- Any middleware, library, or counter that would throttle repeated calls.

What to do:
1. Identify the sensitive endpoints listed above, and any similar abusable actions.
2. For each, check whether a server-side mechanism limits how often it can be called per user or IP — a rate limiter, attempt counter, or lockout. Client-side debouncing does not count.
3. Flag endpoints that can be called an unlimited number of times with no throttle.

Report back:
- The endpoints you checked.
- Any sensitive endpoint with no server-side rate limiting or lockout — name the exact file and route.
- For each, one plain sentence on what it would mean in practice — for example, that the endpoint can be called without limit, allowing automated password or code guessing.
- If the sensitive endpoints have server-side rate limiting, say so plainly and note the mechanism and routes you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

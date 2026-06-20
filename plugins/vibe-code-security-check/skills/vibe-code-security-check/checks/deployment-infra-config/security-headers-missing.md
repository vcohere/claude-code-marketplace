---
category: Deployment & Infra Config
severity: medium
prevalence: common
---

# Baseline security headers absent

Check whether the application sets baseline security response headers.

Where to look:
- Response header configuration: framework config (for example, Next.js headers), middleware, server config, and platform/CDN settings.

What to do:
1. Check for the presence of these response headers on the app's pages and API responses:
   - `Content-Security-Policy`
   - `Strict-Transport-Security`
   - `X-Frame-Options` (or `frame-ancestors` within a CSP)
   - `X-Content-Type-Options`
2. Note which are present and which are absent.
3. Treat this as a configuration check on the response headers themselves; report presence and absence factually.

Report back:
- Where header configuration lives and what you checked.
- Which of the baseline headers are absent.
- For each absent header, one plain sentence on what it covers in practice — for example, that without `X-Frame-Options`/`frame-ancestors` the app can be embedded in another site's frame.
- If all the baseline headers are present, say so plainly and note where they are set.

Do not suggest fixes or assign severity. Report only what you find, with exact configuration references.

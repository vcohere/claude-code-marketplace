---
category: Deployment & Infra Config
severity: medium
prevalence: occasional
---

# CORS allows any origin with credentials

Check whether the API's CORS configuration allows any origin, particularly in combination with credentialed requests.

Where to look:
- CORS configuration in middleware, route handlers, framework config, or platform settings.
- The headers `Access-Control-Allow-Origin` and `Access-Control-Allow-Credentials`.

What to do:
1. Find where CORS headers are set.
2. Check whether `Access-Control-Allow-Origin` is set to `*` or reflects the incoming `Origin` header without an allow-list.
3. Check whether that is combined with `Access-Control-Allow-Credentials: true`, which lets any site make authenticated cross-origin calls in a logged-in user's context.
4. Flag wildcard or reflected origins, and especially the combination with credentials.

Report back:
- The CORS configuration you checked.
- Any wildcard or reflected origin, and whether credentials are also allowed — name the exact file/middleware and the header values.
- For each, one plain sentence on what it would mean in practice — for example, that any website a logged-in user visits could call the API as that user.
- If CORS is restricted to a defined origin allow-list, say so plainly and note where it is configured.

Do not suggest fixes or assign severity. Report only what you find, with exact file and header references.

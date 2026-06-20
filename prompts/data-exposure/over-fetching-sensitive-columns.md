---
category: Data Exposure
severity: medium
prevalence: common
---

# Responses leak sensitive columns the UI never shows

Check whether any endpoint returns sensitive fields to the client that the interface never displays and the requester should not receive.

Where to look:
- Queries and serializers that return user or business records to the client.
- Uses of `select('*')`, returning whole row/document objects, or APIs that echo full records.

What to do:
1. Inspect the actual response payloads sent to the client, not the rendered UI.
2. Look for sensitive fields riding along in those payloads: password hashes, reset/verification tokens, session tokens, internal flags like `is_admin`, payment-provider customer ids, or other users' email/phone/PII.
3. Flag endpoints that return such fields even though the screen only shows a subset (for example, a profile endpoint that returns the whole row when the page shows only a display name).

Report back:
- The endpoints/queries you checked.
- Any response that includes sensitive fields the client does not need — name the exact file/route and list the fields exposed.
- For each, one plain sentence on what it would mean in practice — for example, that the sensitive values are visible to anyone inspecting the network response, even if the page hides them.
- If the inspected endpoints return only the fields the client needs, say so plainly and list what you checked.

Do not suggest fixes or assign severity. Report only what you find, with exact file/route and field names.

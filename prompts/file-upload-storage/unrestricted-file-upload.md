---
category: File Upload & Storage
severity: medium
prevalence: occasional
---

# File uploads accepted with no type, size, or auth limits

Check whether file-upload endpoints validate file type, size, and authentication, and whether uploaded files can be served back in a way that executes or overwrites others' files.

Where to look:
- Upload handlers (API routes, serverless functions) and direct-to-storage upload configuration.
- Any allow-list of MIME types/extensions, size limits, and auth checks on those handlers.

What to do:
1. Find every upload path.
2. For each, check whether it requires authentication, enforces a file-type allow-list, and caps file size.
3. Check whether uploaded content can later be served inline in a way that executes (for example, `.svg` or `.html` served with a renderable content type) or whether a user can overwrite another user's file via predictable paths.
4. Flag handlers missing type, size, or auth validation.

Report back:
- The upload paths you checked.
- Any handler missing type, size, or auth validation, or that serves uploads in an executable way — name the exact file and route, and which checks are absent.
- For each, one plain sentence on what it would mean in practice — for example, that arbitrary or oversized files could be uploaded, or that an uploaded file could run script when viewed by others.
- If every upload path validates type, size, and auth and serves files safely, say so plainly and list what you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and route names.

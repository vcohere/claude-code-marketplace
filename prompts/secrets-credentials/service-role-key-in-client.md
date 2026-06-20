---
category: Secrets & Credentials
severity: critical
prevalence: occasional
---

# Backend service-role / admin key shipped to the browser

Check whether any backend "service role" or admin database key — one that bypasses all access rules — is shipped to the browser.

Where to look:
- Client-side code and the built JavaScript bundle (React/Vite/Next.js frontend files).
- Environment variables exposed to the client: anything prefixed `NEXT_PUBLIC_`, `VITE_`, or otherwise embedded at build time.
- Supabase `createClient` calls, Firebase Admin SDK initialization, and any `*_SERVICE_ROLE_*`, `*_ADMIN_*`, or private-key references.

What to do:
1. Distinguish the public/anon key (intended to be visible in the client) from the service-role / admin key (intended to stay server-only). Only the latter is a finding.
2. Search client-shipped code and bundles for a Supabase `service_role` JWT, Firebase Admin credentials / `FIREBASE_PRIVATE_KEY`, or any other key documented to override access rules.
3. Check whether such a key is passed into a client-side SDK initializer or exposed through a build-time public env variable.

Report back:
- Where you looked (client files, env config, bundle).
- Any service-role/admin key reachable from the client — name the exact file and variable, and confirm it is the privileged key, not the public anon key.
- For each, one plain sentence on what it would mean in practice — for example, that anyone opening browser devtools could use the key to read, change, or delete the entire database regardless of any access policy.
- If no privileged backend key is exposed to the client, say so plainly and note what you inspected.

Do not suggest fixes or assign severity. Report only what you find, with exact file and variable names.

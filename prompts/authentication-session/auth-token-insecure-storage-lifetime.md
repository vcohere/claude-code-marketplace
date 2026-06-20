---
category: Authentication & Session Handling
severity: medium
prevalence: common
---

# Session tokens stored or scoped insecurely

Check how session and access tokens are stored and scoped — where they live, how long they last, and whether logout invalidates them.

Where to look:
- Auth SDK configuration and token handling (Supabase, Firebase, or custom).
- Where tokens are stored (`localStorage`, `sessionStorage`, cookies and their flags), token lifetime/rotation settings, and the logout implementation.

What to do:
1. Determine where access/refresh tokens are stored. Note if they are in `localStorage` (readable by any script running on the page) versus secure, `HttpOnly` cookies.
2. Check token lifetime and whether refresh/rotation is configured, or whether tokens are long-lived with no rotation.
3. Check whether logout invalidates the session server-side or only clears client state.
4. Flag insecure storage, long-lived non-rotating tokens, or logout that leaves the token valid.

Report back:
- The token storage, lifetime, and logout handling you checked.
- Any weakness found — name the exact file/config and describe it (storage location, lifetime, logout behavior).
- For each, one plain sentence on what it would mean in practice — for example, that a script able to read the token could reuse it to act as the user.
- If tokens are stored and scoped securely with proper logout invalidation, say so plainly and note what you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and config references.

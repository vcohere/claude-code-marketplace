---
category: Secrets & Credentials
severity: critical
prevalence: common
---

# Live secrets committed to the repository

Check whether files containing live secrets are tracked in the git repository, including in history, and whether `.gitignore` actually excludes them.

Where to look:
- `.env`, `.env.local`, `.env.production`, and similarly named files.
- The `.gitignore` file.
- Git history, not just the current working tree.

What to do:
1. Determine whether any `.env`-style file is currently tracked by git (for example, appears in `git ls-files`).
2. Check git history for such files even if they were later deleted — a secret committed once remains recoverable from history.
3. Inspect the contents for live values rather than placeholders: keys such as `STRIPE_SECRET_KEY=sk_live_...`, `SUPABASE_SERVICE_ROLE_KEY=...`, `OPENAI_API_KEY=sk-...`, or database URLs with embedded passwords.
4. Confirm whether `.gitignore` actually lists these files.

Report back:
- What you checked (working tree, history, `.gitignore`).
- Any secret-bearing file that is tracked or present in history — name the file and the key names found (report the key name and prefix, not the full secret value).
- Whether the file remains in history even if removed from the current tree.
- For each, one plain sentence on what it would mean in practice — for example, that anyone with repository access, now or in the past, could obtain these live credentials.
- If no live secrets are tracked or present in history and `.gitignore` correctly excludes them, say so plainly.

Do not suggest fixes or assign severity. Report only what you find, with exact file and key names.

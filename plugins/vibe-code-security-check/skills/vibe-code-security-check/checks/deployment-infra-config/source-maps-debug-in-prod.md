---
category: Deployment & Infra Config
severity: medium
prevalence: occasional
---

# Debug mode or server internals exposed in production

Check whether the production build ships with debug mode enabled or exposes server-side source maps or detailed error pages that reveal backend logic.

Where to look:
- Build configuration (for example, `next.config.js`, Vite config), `NODE_ENV`/environment settings, and deploy configuration.
- Settings such as server source map generation, debug flags, and development error overlays.

What to do:
1. Check whether the production build runs with debug/development settings rather than production (for example, `NODE_ENV` not set to `production`, or a debug flag left on).
2. Check whether server-side source maps are emitted for production, or whether a detailed development error overlay is reachable in production.
3. Distinguish normal, expected client bundles (which are always visible) from genuinely leaked server-side logic or configuration.
4. Flag configuration that exposes backend internals in production.

Report back:
- The build/deploy configuration you checked.
- Any debug setting or server source map / dev error page exposed in production — name the exact config file and flag, and what it reveals.
- For each, one plain sentence on what it would mean in practice — for example, that production responses expose backend source or internal structure.
- If the production build disables debug settings and does not expose server internals, say so plainly and note what you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact config references.

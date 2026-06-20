---
category: Input Validation & Injection
severity: high
prevalence: common
---

# User content rendered as raw HTML (stored XSS)

Check whether any user-controlled content is rendered as raw HTML without sanitization.

Where to look:
- React `dangerouslySetInnerHTML`, Vue `v-html`, and direct `innerHTML` assignments.
- Rich-text, comment, markdown, or profile fields whose content comes from users.

What to do:
1. Find every site that renders a value as raw HTML.
2. For each, trace whether the value is user-controlled (stored or reflected) and whether it passes through a sanitizer before rendering.
3. Flag any raw-HTML render bound to user data with no sanitization step.

Report back:
- The raw-HTML render sites you checked.
- Any site that renders unsanitized user content as HTML — name the exact file and component, and the data field involved.
- For each, one plain sentence on what it would mean in practice — for example, that a user could store markup that executes script in another user's browser session when that content is displayed.
- If every raw-HTML render is either not user-controlled or passed through sanitization, say so plainly and list what you checked.

Do not suggest fixes or assign severity. Report only what you find, with exact file and component references.

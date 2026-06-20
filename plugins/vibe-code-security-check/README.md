# Vibe Code Security Check

31 focused security checks for apps built with AI and low-code tools (Lovable, Bolt, Replit, v0, Cursor). Runs as a full sweep or one check at a time. Detection and reporting only — no fixes applied.

## Install

Add the marketplace and install the plugin directly in Claude Code:

```
/plugin marketplace add vcohere/claude-code-marketplace
/plugin install vibe-code-security-check@logique-marketplace
```

### Or clone locally for development

```bash
git clone https://github.com/vcohere/claude-code-marketplace.git
cd claude-code-marketplace

/plugin marketplace add ./

/plugin install vibe-code-security-check@logique-marketplace
```

## Usage

From any Claude Code session with your project open:

```
/vibe-code-security-check
```

Claude Code runs every check in `checks/` against your codebase and returns one consolidated report grouped by category, most severe findings first.

**When to run it:** treat this like a pre-launch or pre-release sweep, not a daily tool. Running 31 checks in one pass is context-intensive — it reads broadly across your codebase for each check, which adds up. Good trigger points: before you go live, after a significant feature addition, or when you onboard a new backend integration. For routine development, run individual checks instead (see below).

### Run a single check

Open any file under [`checks/`](./skills/vibe-code-security-check/checks/), copy its full contents, and paste it to Claude Code with your project open. Each check is self-contained — no setup needed.

## What's covered

| Category                          | Checks | What it looks at                                                                                              |
| --------------------------------- | -----: | ------------------------------------------------------------------------------------------------------------- |
| Authentication & Session Handling |      2 | Whether identity is established securely and tokens are stored and scoped safely.                             |
| Authorization & Access Control    |      4 | Whether the app enforces who can read or write which data, beyond just being logged in.                       |
| Secrets & Credentials             |      3 | Whether backend keys and credentials are kept off the client and out of the repo.                             |
| Data Exposure                     |      2 | Whether responses and endpoints return rows or columns the requester shouldn't see.                           |
| Input Validation & Injection      |      3 | Whether untrusted input can reach a query, an LLM prompt, or the page in a way that executes or exfiltrates. |
| Client-Side Trust                 |      2 | Whether security or revenue decisions are enforced only in the browser, and therefore bypassable.             |
| API & Backend Surface             |      2 | Whether backend write endpoints require auth and abusable endpoints are rate limited.                         |
| Third-Party Integration Misconfig |      2 | Whether integrations like payments and OAuth verify and constrain what they trust.                            |
| File Upload & Storage             |      2 | Whether file storage is private and uploads are validated and safe to serve.                                  |
| Payment & Financial Flows         |      2 | Whether the money path is tamper-proof and access is granted only on confirmed payment.                       |
| Abuse & Cost Runaway              |      1 | Whether billable operations are metered so one actor can't run up the bill.                                   |
| Logging & PII Leakage             |      2 | Whether errors and logs leak internals, secrets, or personal data.                                            |
| Dependency & Supply Chain         |      1 | Whether shipped dependencies carry known-exploitable vulnerabilities.                                         |
| Deployment & Infra Config         |      3 | Whether production config (CORS, headers, debug mode) leaves a gap.                                          |

## Why detection only, no fixes

Security fixes are surgical — the right change depends on context, framework, and choices only you know. Auto-applying fixes without review creates a different risk: a change that looks correct in isolation but breaks surrounding logic, or silently alters behavior you were relying on. The report gives you the exact location and what it means in practice; from there you decide how to fix it, and can ask Claude to help with specific findings one at a time in a fresh session. Keeping sweep and fix separate also makes the report easier to audit and share with a team.

## Who made this

Built by [Logique](https://logique.io) — security hardening for founders who built and shipped apps on AI and low-code platforms.

## License

MIT

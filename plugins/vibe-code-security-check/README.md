# Vibe Code Security Check

31 focused security checks for apps built with AI and low-code tools (Lovable, Bolt, Replit, v0, Cursor). Runs as a full sweep or one check at a time. Detection and reporting only — no fixes applied.

## Install

### Via marketplace

```bash
git clone https://github.com/vcohere/claude-code-marketplace.git .claude/logique-marketplace
mkdir -p .claude/commands

cat > .claude/commands/vibe-code-security-check.md << 'EOF'
Follow the instructions in .claude/logique-marketplace/plugins/vibe-code-security-check/skills/vibe-code-security-check/SKILL.md.
The checks/ folder referenced in that file is at .claude/logique-marketplace/plugins/vibe-code-security-check/skills/vibe-code-security-check/checks/.
EOF
```

### Manual (plugin only)

```bash
git clone https://github.com/vcohere/claude-code-marketplace.git .claude/logique-marketplace
mkdir -p .claude/commands

cat > .claude/commands/vibe-code-security-check.md << 'EOF'
Follow the instructions in .claude/logique-marketplace/plugins/vibe-code-security-check/skills/vibe-code-security-check/SKILL.md.
The checks/ folder referenced in that file is at .claude/logique-marketplace/plugins/vibe-code-security-check/skills/vibe-code-security-check/checks/.
EOF
```

## Usage

From any Claude Code session with your project open:

```
/vibe-code-security-check
```

Claude Code runs every check in `checks/` against your codebase and returns one consolidated report grouped by category, most severe findings first.

To update: `git -C .claude/logique-marketplace pull`

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

## Who made this

Built by [Logique](https://logique.io) — security hardening for founders who built and shipped apps on AI and low-code platforms.

## License

MIT

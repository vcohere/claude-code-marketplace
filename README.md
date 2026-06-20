# Vibe Code Security Check

A set of focused security checks for apps built with AI and low-code tools (Lovable, Bolt, Replit, v0, Cursor). Each check is a single prompt you run on your own coding agent, against your own codebase. They look for the specific, well-known ways apps built this way tend to ship with gaps - exposed keys, open database access, endpoints with no auth, money paths that trust the browser, and so on.

You don't need to read code to use these. You run a prompt, your agent inspects your project, and it reports back in plain language: what it checked, what it found, and where.

**Coverage:** 31 checks across 14 categories.

## How to use it

You can run a single check, or sweep all of them at once.

### Run one check

1. Open any file in [`prompts/`](./prompts).
2. Copy its full contents.
3. Paste it to your coding agent (Claude Code, Cursor) with your project open.

The agent will inspect your codebase for that one issue and report back. Each prompt is self-contained - no setup, no context needed beyond your repo being open.

### Run all of them

This repo includes a Skill, `vibe-code-security-check`, that runs every check in `prompts/` against your codebase and produces one consolidated report - grouped by category, most severe findings first, with the clean results listed too so you can see full coverage.

Point your agent at this repo and ask it to run the `vibe-code-security-check` skill against your project. It discovers every check on disk at run time, so the sweep always reflects whatever's in `prompts/`.

The checks are detection and reporting only. Nothing here changes your code — it tells you what it finds and leaves the fixing to you.

## What's covered

| Category                          | Checks | What it looks at                                                                                             |
| --------------------------------- | -----: | ------------------------------------------------------------------------------------------------------------ |
| Authentication & Session Handling |      2 | Whether identity is established securely and tokens are stored and scoped safely.                            |
| Authorization & Access Control    |      4 | Whether the app enforces who can read or write which data, beyond just being logged in.                      |
| Secrets & Credentials             |      3 | Whether backend keys and credentials are kept off the client and out of the repo.                            |
| Data Exposure                     |      2 | Whether responses and endpoints return rows or columns the requester shouldn't see.                          |
| Input Validation & Injection      |      3 | Whether untrusted input can reach a query, an LLM prompt, or the page in a way that executes or exfiltrates. |
| Client-Side Trust                 |      2 | Whether security or revenue decisions are enforced only in the browser, and therefore bypassable.            |
| API & Backend Surface             |      2 | Whether backend write endpoints require auth and abusable endpoints are rate limited.                        |
| Third-Party Integration Misconfig |      2 | Whether integrations like payments and OAuth verify and constrain what they trust.                           |
| File Upload & Storage             |      2 | Whether file storage is private and uploads are validated and safe to serve.                                 |
| Payment & Financial Flows         |      2 | Whether the money path is tamper-proof and access is granted only on confirmed payment.                      |
| Abuse & Cost Runaway              |      1 | Whether billable operations are metered so one actor can't run up the bill.                                  |
| Logging & PII Leakage             |      2 | Whether errors and logs leak internals, secrets, or personal data.                                           |
| Dependency & Supply Chain         |      1 | Whether shipped dependencies carry known-exploitable vulnerabilities.                                        |
| Deployment & Infra Config         |      3 | Whether production config (CORS, headers, debug mode) leaves a gap.                                          |

Checks are organized into one folder per category under [`prompts/`](./prompts).

## What this is and isn't

These checks surface the failure modes that show up most often in apps built quickly with AI tools. They're a practical first pass, not a full audit.

A clean result on a given check means _that specific issue_ wasn't found - not that your app is secure overall. The checks don't know your business logic, they can't see every path through your code, and some need access (a live database, a deployed environment) that your agent may not have when it runs. Where a check can't fully verify something, it's built to say so rather than guess.

Use this to catch the obvious, high-impact problems early. Treat a clean sweep as "the common doors are closed," not "nothing was missed."

## Who made this

This was put together by [Logique](https://logique.io), where I do security hardening for founders who built and shipped apps on AI and low-code platforms. The checks here are the kind of thing I look for first.

If you'd rather have an engineer verify the whole codebase end to end - instead of guessing which checks to run and interpreting the results yourself - then [let's chat](https://calendly.com/logiquelabs/general-project-chat)

## License

MIT - use them, fork them, adapt them. If they're useful, a link back is appreciated but not required.

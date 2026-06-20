# Logique Marketplace

A Claude Code marketplace of security and code-quality skills, maintained by [Logique](https://logique.io).

## Quick Start

### Add this marketplace to Claude Code

```
/plugin marketplace add vcohere/claude-code-marketplace
```

### Install a plugin

```
/plugin install vibe-code-security-check@logique-marketplace
```

### Or clone locally for development

```bash
git clone https://github.com/vcohere/claude-code-marketplace.git
cd claude-code-marketplace

/plugin marketplace add ./

/plugin install vibe-code-security-check@logique-marketplace
```

---

## Plugins

| Plugin | Category | Description | Version |
| ------ | -------- | ----------- | ------- |
| [vibe-code-security-check](./plugins/vibe-code-security-check/) | Security | 31 security checks across 14 categories for apps built with AI/low-code tools | 1.0.0 |

---

### vibe-code-security-check

31 focused security checks for apps built with AI and low-code tools — Lovable, Bolt, Replit, v0, Cursor. Covers authentication, authorization, secrets exposure, injection, payment flows, and more. Runs as a full sweep or one check at a time. Detection and reporting only.

[Install & usage →](./plugins/vibe-code-security-check/README.md)

---

## Contributing

To add a plugin to this marketplace:

1. Fork this repo.
2. Create `plugins/<your-plugin-name>/` with the following structure:
   ```
   plugins/<your-plugin-name>/
   ├── .claude-plugin/
   │   └── plugin.json
   ├── skills/
   │   └── <skill-name>/
   │       └── SKILL.md
   └── README.md
   ```
3. Add an entry for your plugin to `.claude-plugin/marketplace.json`.
4. Open a pull request.

See an existing plugin (e.g. [`vibe-code-security-check`](./plugins/vibe-code-security-check/)) for reference.

## License

MIT

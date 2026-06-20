---
category: Dependency & Supply Chain
severity: medium
prevalence: common
---

# Dependencies with known exploitable vulnerabilities

Check whether shipped dependencies include versions with known critical or high-severity vulnerabilities, or risky version practices.

Where to look:
- Lockfiles and manifests: `package-lock.json`, `yarn.lock`, `pnpm-lock.yaml`, `package.json`.
- Version ranges declared in the manifest.

What to do:
1. Inspect installed dependency versions against known advisories (for example, run the package manager's audit and/or check installed versions against published CVEs).
2. Surface dependencies carrying known critical/high advisories (such as remote code execution or prototype pollution) rather than the full noise of every low-severity item.
3. Note risky version practices such as wildcard ranges (`"lib": "*"`) or unpinned installs that pull unvetted updates.
4. Where possible, note whether a flagged package appears to be actually used in the app.

Report back:
- What you inspected and how (audit tool, manifest review).
- Any dependency with a known critical/high advisory — name the package, the installed version, and the advisory id.
- Any wildcard or unpinned version ranges — name the package and the range.
- For each, one plain sentence on what it would mean in practice — for example, that the installed version is subject to a published exploit.
- If no critical/high advisories are present and versions are pinned sensibly, say so plainly and note what you checked.

Do not suggest fixes. Report only what you find — name the package, version, and advisory id as published, without adding your own ranking.

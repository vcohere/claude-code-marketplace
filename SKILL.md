---
name: vibe-code-security-check
description: Run a full security check sweep across every prompt in this repo's prompts/ directory against the current codebase, aggregate the results, and produce one consolidated plain-language report grouped and ordered by severity. Use when someone wants a complete security pass rather than running individual check files one at a time.
---

# Vibe Code Security Check

Run every check defined in this repo's `prompts/` directory against the current codebase and produce a single consolidated report. This skill is detection and reporting only.

## Scope

- **Checks** live in this skill repo, under `prompts/` (one `.md` file per check, in category subfolders). Each file carries `category`, `severity`, and `prevalence` in YAML frontmatter at the top.
- **The target** of every check is the _current codebase the agent is sitting in_ — the user's project — not this skill repo.

## Procedure

### 1. Discover the checks dynamically

Enumerate every `.md` file under `prompts/`, recursively, at run time. Do not hardcode filenames, ids, or counts — the set of checks is whatever exists on disk at the moment of the run, so files added or removed later are picked up automatically. For each file, derive its id from the filename without the `.md` extension and read its `category`, `severity`, and `prevalence` from the file's YAML frontmatter.

### 2. Run each check

For each discovered file, treat the body below the frontmatter as a self-contained instruction set and carry it out against the current codebase. The frontmatter (`category`, `severity`, `prevalence`) is metadata for aggregation only — do not echo it in findings. Each check is independent — run it on its own, with no shared state or context carried between checks. Follow each prompt exactly as written, including its own instruction to report findings without proposing fixes.

### 3. Record a single status per check

For each check, capture exactly one outcome:

- **finding** — the check identified a problem. Record the exact location(s) the prompt asked for (file, route, table, policy, config, etc.) and the one-sentence plain-English "what it means in practice" that the prompt itself instructs the agent to produce.
- **clean** — the check ran fully and found nothing. Keep it; clean checks are listed explicitly so coverage is visible.
- **could-not-verify** — the check could not be completed (relevant files absent, framework not present, no access to the live resource it needs, ambiguous evidence). Note briefly why.

### 4. Order and group by frontmatter

Build one consolidated report — not a concatenation of per-check reports.

- **Group** every check under its `category` from the file's frontmatter.
- **Order** so the most severe findings surface first: within the report, present categories and checks so that `critical` comes before `high`, which comes before `medium`. Within a single group, order checks by severity the same way.
- If a discovered file is **missing frontmatter** or any of those fields, do not fail. Place it **last within its group** (and, lacking a category, group it under an "Uncategorized" section placed last), and label its severity as unknown.

For each category, list its findings first (most severe first), then the clean checks, then any could-not-verify checks, so coverage within the category is fully visible.

### 5. Detection and reporting only

Never propose, suggest, or apply fixes, and never assign or re-rank severity beyond what each prompt's frontmatter already states. This holds at the aggregate level just as it does inside each individual prompt. Report only what was found, with the exact locations the prompts asked for.

### 6. Close with a summary block

End the report with totals:

- total checks run
- count with a finding
- count clean
- count could-not-verify

## Tone

Operational and neutral throughout, matching the prompt files. No urgency language and no marketing framing anywhere.

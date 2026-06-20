---
category: Input Validation & Injection
severity: high
prevalence: occasional
---

# User input injected into an LLM prompt with broad access

Check whether features that send user input to an LLM keep untrusted input separate from instructions, and whether the model can reach tools or data the user should not control.

Where to look:
- Code that builds prompts for an LLM (OpenAI, Anthropic, or similar) and sends user-provided text.
- Any tools, functions, or data access granted to the model (database queries, internal APIs, file access).

What to do:
1. Find where user input is incorporated into a prompt. Check whether it is concatenated directly into the system/instruction portion (for example, `systemPrompt + userInput`) versus kept in a separate, clearly delimited user role with the instructions fixed server-side.
2. Identify what the model can do or reach: which tools/functions it can call and what data those touch.
3. Flag cases where user input can override the instructions and the model has access to data or actions the user should not be able to direct (for example, a tool that can read other users' records, reachable through model output).

Report back:
- The LLM features, prompt-construction sites, and model tool/data access you checked.
- Any feature where untrusted input is merged into instructions and the model can reach sensitive data or actions — name the exact file and describe what the model can reach.
- For each, one plain sentence on what it would mean in practice — for example, that crafted input could direct the model to return or act on data beyond the user's own.
- If user input is properly separated from instructions and model access is constrained, say so plainly and list what you checked.

Do not suggest fixes or assign severity. Report only what you find, with exact file references.

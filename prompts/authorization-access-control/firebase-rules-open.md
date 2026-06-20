---
category: Authorization & Access Control
severity: critical
prevalence: common
---

# Firebase security rules left open

Check whether Firebase security rules (Firestore, Realtime Database, and Storage) restrict access per user rather than leaving data open or merely gated on being signed in.

Where to look:
- `firestore.rules`, `database.rules.json`, `storage.rules`, and any rules referenced in `firebase.json`.

What to do:
1. Read each rules file and find every `match` block governing user or business data.
2. Flag permissive patterns such as `allow read, write: if true` (open to anyone) and recursive wildcard matches like `match /{document=**}` granting broad access.
3. Flag rules gated only on `request.auth != null` for collections holding per-user data — this allows any signed-in user to read or write every other user's documents, which is different from scoping access to the document's owner.
4. Check that database rules and Storage rules are both evaluated, not just one of them.

Report back:
- The rules files and match blocks you checked.
- Any block that is fully open, or gated only on "is signed in" where the data is per-user — name the file and quote the offending match/allow block.
- For each, one plain sentence on what it would mean in practice — for example, that any visitor, or any logged-in user, could read or modify documents belonging to other users.
- If every rule scopes access to the owning user, say so plainly and list the blocks you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact file and rule references.

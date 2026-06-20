---
category: File Upload & Storage
severity: high
prevalence: common
---

# User-file storage bucket is public

Check whether storage buckets holding user files are publicly readable or listable.

Where to look:
- Supabase Storage bucket configuration, Firebase Storage rules, and S3 bucket policies / ACLs.
- Bucket definitions in config, migrations, or infrastructure files, and the kind of files each bucket holds.

What to do:
1. Enumerate the storage buckets and identify which hold user-uploaded files (IDs, invoices, documents, private images, etc.).
2. For each, determine whether it is public-read (for example, `public = true`, or a Storage rule `allow read: if true`) and whether listing is enabled.
3. Flag buckets holding user files that are reachable by anyone with — or guessing — the URL, independent of the app's login.

Report back:
- The buckets you checked and what they hold.
- Any bucket holding user files that is public-read or listable — name the bucket and its configuration.
- For each, one plain sentence on what it would mean in practice — for example, that the files are reachable directly by URL without authenticating to the app.
- If every bucket holding user files is private, say so plainly and list the buckets you verified.

Do not suggest fixes or assign severity. Report only what you find, with exact bucket names and settings.

# Agent Instructions

Always commit and push completed changes to `main`, unless David explicitly asks not to push.

This repo is a public, client-friendly progress feed for Studio Prime dashboards.

- Keep one JSON file per client, named by client slug.
- Set the top-level `lang` field and write all client-facing text in that language.
- Current client feeds `dooctoor.json` and `grupo-husdrommer.json` must be Spanish-only (`"lang": "es"`).
- Keep all content safe for clients to read.
- Do not include private notes, credentials, raw internal blockers, technical implementation details, or private attachments.
- Every progress item must include `createdAt` and `doneAt` as `YYYY-MM-DD` dates. Use `doneAt: null` until the item is done.
- When an item is complete, set `status: "done"` and fill `doneAt` so dashboards can hide done items older than one month.
- Use these board sections and statuses: `backlog`, `next`, `needs_client`, `in_review`, `done`. In Spanish, label `needs_client` as "Necesita tu ayuda".
- Keep files valid against `schema.json`.

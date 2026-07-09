# Agent Instructions

Always commit and push completed changes to `main`, unless David explicitly asks not to push.

This repo is a public, client-friendly progress feed for Studio Prime dashboards.

- Keep one JSON file per client, named by client slug.
- Set the top-level `lang` field and write all client-facing text in that language.
- Current client feeds `dooctoor.json` and `grupo-husdrommer.json` must be Spanish-only (`"lang": "es"`).
- Keep all content safe for clients to read.
- Do not include private notes, credentials, raw internal blockers, technical implementation details, or private attachments.
- Every progress item must include a stable integer `number` that clients and David can use as a shared reference. Numbers are per client and should increase from the highest existing number; imported GitHub tasks keep their original GitHub issue/task number.
- Every progress item must include an `app` object with `key`, `label`, and `emoji`. Identify the concrete client app/product the task belongs to before creating it, for example Dooctoor apps like `colegios`, `farmacias`, `personal`, `backoffice`, or `marketing`. Use `key: "core"` only for tasks that affect the whole client workspace or multiple apps.
- Every progress item must include `createdAt` and `doneAt` as `YYYY-MM-DD` dates. Use `doneAt: null` until the item is done.
- When an item is complete, set `status: "done"` and fill `doneAt` so dashboards can hide done items older than one month.
- Use these board sections and statuses: `backlog`, `next`, `needs_client`, `in_review`, `done`. In Spanish, label `needs_client` as "Necesita tu ayuda".
- Start every client-facing progress item `title` with one friendly, relevant emoji.
- Keep files valid against `schema.json`.

# Agent Instructions

Always commit and push completed changes to `main`, unless David explicitly asks not to push.

This repo is a public, client-friendly progress feed for Studio Prime dashboards.

- Keep one JSON file per client, named by client slug.
- Set the top-level `lang` field and write all client-facing text in that language.
- Current client feeds `dooctoor.json` and `grupo-husdrommer.json` must be Spanish-only (`"lang": "es"`).
- Keep all content safe for clients to read.
- Do not include private notes, credentials, raw internal blockers, technical implementation details, or private attachments.
- Do not publish a client task from raw material by assumption alone. The matching internal task in `../client-docs/` must first be contrasted against the relevant code/product state or confirmed by David.
- Do not publish ambiguous cross-client or cross-app mentions. If a source document appears to belong to one client/app but contains lines that may refer to another, keep that interpretation in `../client-docs/` as blocked `Need From David` until David confirms it.
- Every progress item must include a stable integer `number` that clients and David can use as a shared reference. Numbers are per client and should increase from the highest existing number; imported GitHub tasks keep their original GitHub issue/task number.
- Mark task type with optional `kind`: use `"request"` for normal requests, `"bug"` for client-reported broken behavior, and `"question"` for explicit doubts/decision items. `kind: "bug"` means reported bug until Codex reproduces or verifies it; do not write as if confirmed unless evidence/code/testing confirms it. Bug checklists should include reproduction or verification before fix work.
- Every progress item must include an `app` object with `key`, `label`, and `emoji`. Identify the concrete client app/product the task belongs to before creating it, for example Dooctoor apps like `colegios`, `farmacias`, `personal`, `backoffice`, or `marketing`. Use `key: "core"` only for tasks that affect the whole client workspace or multiple apps.
- Client-safe attachments can be included with an `attachments` array. Use `type: "pdf"`, `"image"`, `"doc"`, `"sheet"`, or `"link"` plus a short `label` and `url`. Store public files under `assets/<client-slug>/...` and reference that relative path. Use external `https://` links only when the linked resource is safe for clients. Attachments should open in browser preview where possible; avoid raw download URLs for PDFs, images, Word, and Excel files.
- After editing a JSON feed, verify every local attachment URL exists in this repo and that the number of public attachments is the intended client-safe subset from `../client-docs/`. Do not publish screenshots/files containing private notes, PII, credentials, or sensitive client context. If an expected attachment cannot be copied, read, or safely published, record the gap in `../client-docs/` and tell David.
- Every progress item must include `createdAt` and `doneAt` as `YYYY-MM-DD` dates. Use `doneAt: null` until the item is done.
- When an item is complete, set `status: "done"` and fill `doneAt` so dashboards can hide done items older than one month.
- Use these board sections and statuses: `backlog`, `next`, `needs_client`, `in_review`, `done`. In Spanish, label `needs_client` as "Necesita tu ayuda".
- Start every client-facing progress item `title` with one friendly, relevant emoji.
- Do not repeat the client/app name in client-facing item titles when the `app` badge already shows it. Prefer `🧭 Actualización de estructura y contenidos` over `🧭 Atelia · Actualización de estructura y contenidos`.
- Prefer short client-facing items with a `checklist` over long descriptions. The dashboard should make it easy for clients to see what will happen, not expose internal reasoning.
- Keep `summary` and `nextStep` short and client-safe when present. They are supporting copy, not a place for uncertainty, implementation notes, or messages to David.
- Do not store hidden/internal context in this public repo. Anything "for Codex only" or "for David" belongs in `../client-docs/`, even if the Studio Prime dashboard would not render that field.
- Keep files valid against `schema.json`.

## Email-Derived Progress

- Only publish email-derived tasks after the full email/thread and all relevant attachments have been read and understood.
- If any source content, link, or attachment could not be fully read, do not present the task as confidently ready in public progress; keep the missing context in `client-docs` and use `needs_client` only when the client-facing next step is clear and safe.
- Never expose sender details, private email text, internal reasoning, private attachments, or technical uncertainty in this public repo.
- If a client request appears contradictory, impossible, or inconsistent with the product/code, keep the concern in `client-docs` for David instead of publishing a polished but misleading public task.
- If an attachment contains confusing mentions outside the apparent client/app, do not smooth it into a public task. Keep it internal/blocked until David clarifies.

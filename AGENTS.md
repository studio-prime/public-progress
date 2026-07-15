# Agent Instructions

Always commit and push completed changes to `main`, unless David explicitly asks not to push.

This repo is a public, client-friendly generated progress feed for Studio Prime dashboards.

## Generated Repository

Do not edit JSON feeds, `schema.json`, or copied assets in this repository by hand. The private `../client-docs/` repository is the single source of truth:

- Edit `../client-docs/clients/<client-slug>/client.json`, the canonical `projects.json` and `milestones.json`, and private task sources named `tasks/<REFERENCE>-<descriptive-slug>.md`.
- Keep client-safe content inside the task's explicit `public` frontmatter object. Universal task dates belong in the private source `lifecycle` object, not in `public`; the generator derives this repository's `createdAt` and `doneAt` fields.
- Never copy the task's private `internal` object or Markdown body into this repository.
- Run `node scripts/generate.mjs` from `../client-docs/` to rebuild this repository.
- Run `node scripts/generate.mjs --check` before committing.
- `changelog/<client-slug>.json` is generated from completed public tasks; do not edit it directly.
- `projects/<client-slug>.json` is the generated client-safe project catalog; do not edit it directly.
- `milestones/<client-slug>.json` is the generated client-safe milestone progress feed; do not edit it directly or maintain completion percentages by hand.

The rules below define the generated public contract and still apply to source frontmatter.

- Keep one JSON file per client, named by client slug.
- Set the top-level `lang` field and write all client-facing text in that language.
- Current client feeds `dooctoor.json` and `grupo-husdrommer.json` must be Spanish-only (`"lang": "es"`).
- Every client feed must include a unique three-letter uppercase `taskPrefix`, for example `DOO` for Dooctoor and `HUS` for Grupo HusDrommer.
- Keep all content safe for clients to read.
- Do not include private notes, credentials, raw internal blockers, technical implementation details, or private attachments.
- When useful for client trust, include optional `clientContext` with `{ "label": "...", "body": "..." }`. This powers the dashboard's original-request view. It must be short, readable, and sanitized: no sender metadata, private email/thread details, internal reasoning, credentials, PII, Codex notes, or David notes.
- Do not use `clientContext` as raw storage. Summarize or excerpt only the safe parts that directly explain why the task exists.
- Do not publish a client task from raw material by assumption alone. The matching internal task in `../client-docs/` must first be contrasted against the relevant code/product state or confirmed by David.
- Do not publish ambiguous cross-client or cross-app mentions. If a source document appears to belong to one client/app but contains lines that may refer to another, keep that interpretation in `../client-docs/` as `Need From David` when David can decide, or as `Blocked by Client` when only the client/external source can unblock it.
- Every progress item must include a stable integer `number` plus a `reference` built as `<PREFIX>-<number>`, for example `DOO-23`. Clients and David should use the `reference` when discussing work. Numbers are per client and should increase from the highest existing number; imported GitHub tasks keep their original GitHub issue/task number.
- Mark task type with optional `kind`: use `"request"` for normal requests, `"bug"` for client-reported broken behavior, and `"question"` for explicit doubts/decision items. `kind: "bug"` means reported bug until Codex reproduces or verifies it; do not write as if confirmed unless evidence/code/testing confirms it. Bug checklists should include reproduction or verification before fix work.
- Every feed includes its registered client-safe `projects` catalog, and every progress item includes its resolved `projects`. Project identity comes only from private `client-docs` catalogs. Never invent `core`, `grupo`, or a client-level pseudo-project. The generated `app` field is a temporary StudioPrime compatibility field; do not author or edit it here.
- Every feed includes generated milestones, and every progress item includes its resolved milestone reference. Milestone status, task counts, and completion percentage are derived from public task statuses in `client-docs`.
- Client-safe attachments can be included with an `attachments` array. Use `type: "pdf"`, `"image"`, `"doc"`, `"sheet"`, or `"link"` plus a short `label` and `url`. Store public files under `assets/<client-slug>/...` and reference that relative path. Use external `https://` links only when the linked resource is safe for clients. Attachments should open in browser preview where possible; avoid raw download URLs for PDFs, images, Word, and Excel files.
- Internal rendered PDF/page review captures belong in `../client-docs/assets/`, not this public repo, unless David explicitly approves them as client-safe and useful for the dashboard.
- After editing task source frontmatter, run the generator and verify every local attachment URL exists in this repo and that the number of public attachments is the intended client-safe subset from `../client-docs/`. Do not publish screenshots/files containing private notes, PII, credentials, or sensitive client context. If an expected attachment cannot be copied, read, or safely published, record the gap in `../client-docs/` and tell David.
- Every generated progress item must include `createdAt` and `doneAt`. They are derived from private `lifecycle.createdAt` and `lifecycle.completedAt`; keep `lifecycle.completedAt: null` until the item is publicly closed after client/David acceptance.
- Public `in_review` means the work has been internally verified by Codex or David and is ready for the client to review.
- Internal `client-docs` `🧪 Ready for QA` means implementation shipped but the release gate is still pending. Keep it publicly in `next`; never present it as `in_review` or `done` yet.
- Public `done` means the work has been accepted/closed after client or David review. Only then set private `lifecycle.completedAt`; the generator fills `doneAt` so dashboards can hide completed items older than one month.
- Internal `client-docs` `👀 To Review Manually` is not client review. Do not publish those items as `in_review`; keep/move them to `next` with client-safe copy such as "Estamos haciendo una revisión final interna."
- Use these board sections and statuses: `backlog`, `next`, `needs_client`, `in_review`, `done`. In Spanish, use these labels: `backlog` = "Pendiente", `next` = "En progreso", `needs_client` = "Necesita ayuda", `in_review` = "Listo para revisión", `done` = "Completado".
- Internal `Blocked by Client` work should only appear publicly as `needs_client` when the client-facing ask is safe, clear, and useful. Otherwise keep it internal in `../client-docs/`.
- Use emojis only to identify projects. Single-project titles start with the registered project's emoji; cross-project titles start with the generated `🧩` compatibility badge.
- Do not repeat the client/project name in client-facing item titles when the dashboard already shows the project badge. Prefer `🏡 Actualización de estructura y contenidos` over `🏡 Atelia · Actualización de estructura y contenidos`.
- Prefer short client-facing items with a `checklist` over long descriptions. The dashboard should make it easy for clients to see what will happen, not expose internal reasoning.
- Keep `summary` and `nextStep` short and client-safe when present. They are supporting copy, not a place for uncertainty, implementation notes, or messages to David.
- Do not store hidden/internal context in this public repo. Anything "for Codex only" or "for David" belongs in `../client-docs/`, even if the Studio Prime dashboard would not render that field.
- Keep files valid against `schema.json`.

## Email-Derived Progress

- Only publish email-derived tasks after the full email/thread and all relevant attachments have been read and understood.
- If any source content, link, or attachment could not be fully read, do not present the task as confidently ready in public progress; keep the missing context in `client-docs` as `Need From David` or `Blocked by Client` and use public `needs_client` only when the client-facing next step is clear and safe.
- Never expose sender details, private email text, internal reasoning, private attachments, or technical uncertainty in this public repo.
- If a client request appears contradictory, impossible, or inconsistent with the product/code, keep the concern in `client-docs` for David instead of publishing a polished but misleading public task.
- If an attachment contains confusing mentions outside the apparent client/app, do not smooth it into a public task. Keep it internal as `Need From David` or `Blocked by Client` until clarified.

# Public Progress Instructions

This public repository is a generated, client-safe projection of the private
`studio-prime/client-os` operating system.

## Never Edit Generated Data

Do not edit JSON feeds, schema, changelogs, milestones, projects, or copied
assets by hand. Canonical work lives in private GitHub Issues in
`studio-prime/client-os`.

Generate from the sibling private checkout:

```bash
cd ../client-os
npm run generate
npm run generate:check
```

## Safety Boundary

- Export only fields explicitly authored in an Issue metadata `public` object.
- Never infer client-safe copy from private Issue bodies, comments, labels,
  source archives, attachments, agent reasoning, or product PRs.
- `public: null`, `public:hidden`, and Inbox/specification work are not exported.
- Never expose credentials, sender details, private email, personal data,
  internal URLs, implementation notes, David-only decisions, or one client's
  data to another.
- Copy only explicitly declared public attachments and validate every path.
- Keep all output valid against `schema.json`.

## Public Contract

- One top-level JSON file per client slug.
- Client-facing text uses the feed's declared language.
- References remain stable as `<PREFIX>-<number>`.
- Projects and milestones come only from registered private catalogs.
- Supported public statuses remain `backlog`, `next`, `needs_client`,
  `in_review`, and `done`.
- `in_review` means ready for client review.
- `done` requires accepted/closed work and a completion date.
- Reported bugs remain reported until verified.

Only the Studio Prime Release Manager or the audited Client OS sync workflow may
publish. Public progress must be pushed before anyone claims the client-facing
view is current.

# tabby-studio-notices

Public update channel for **Tabby UI Studio**. A running Studio preview fetches
[`notices.json`](notices.json) (raw, CORS-open) to learn whether a newer shell version
is available, and shows an in-preview **"Update available"** banner if so. No secrets,
no code — just a version number and a one-line summary.

Consumed by `apps/studio/src/shell/Broadcast/useBroadcast.ts` in the Studio monorepo.

## `notices.json`

| field | meaning |
| --- | --- |
| `latestShellVersion` | The latest Studio shell version published to the Drawer. |
| `headline` | One-line, designer-facing summary of what that update brings (optional). |

The banner appears in a designer's preview when `latestShellVersion` is **greater than**
the version their Studio is currently running — and stops once they update.

## How it's updated — automatically

**Don't hand-edit this file.** It's written by `tooling/broadcast.mjs` in the Studio
monorepo, which runs at the end of `pnpm publish:drawer`. The version comes from
`apps/studio/package.json` and the headline from the matching `CHANGELOG` entry in
`src/shell/Broadcast/content.ts`. To refresh only the headline without republishing,
run `pnpm broadcast --headline "…"`. The next publish overwrites whatever is here.

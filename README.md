# tabby-studio-notices

Public broadcast channel for **Tabby UI Studio**. A running Studio preview fetches
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

## Updating (do this at each Drawer publish)

When you publish a new shell version to the Drawer:

1. Bump `latestShellVersion` here to the **same** version you bumped
   `apps/studio/package.json` to.
2. Update `headline` to a short, designer-facing summary of the change.

The raw CDN refreshes within ~5 minutes. That's all — no rebuild, no skill reinstall.

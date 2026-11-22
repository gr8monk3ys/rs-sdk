---
status: accepted
date: 2026-11-22
---

# Vendor the LostCity engine, content and webclient in-tree

`server/{engine,content,webclient}` are copies of upstream LostCity (rev 274) with local modifications squashed on top, rather than git submodules or an npm dependency. The SDK needs custom packets, a Bot state collector in the client and the Grand Exchange inside the engine, which no upstream extension point offers.

## Consequences

- Every local modification is listed in `server/PATCHES.md` and must be re-verified after each vendor sync.
- Type-checking and tooling treat these trees separately: the root `tsconfig.json` excludes `server/engine` and `server/webclient`, and the webclient has its own tsconfig.
- Boundary rules (`.dependency-cruiser.cjs`) are baselined for the engine's existing violations; new violations fail `bun run check`.

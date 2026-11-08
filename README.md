# Dhwaja review chunks

Two review bundles, split on file boundaries into chunks of about 300 KB each (roughly 75–90k tokens, which fits models with a 128k context window and leaves room to reply).

## Which set to use

- **server-focused-2026-11-07/** (75 chunks, 785 files): **use this one.** It's the newer snapshot (21:22 UTC) and covers all TS/JS plus the 254 trust-core SQL files.
- **tsjs-only-2026-11-07/** (73 chunks, 536 files): older snapshot (04:18 UTC). 507 of its files are identical to the server set and 24 have changed since. It only adds 5 trust-core test-fidelity files. Keep it for comparison only.

## How the chunks are laid out

- Files appear in repo path order, so each chunk covers one area (an app, a package, or a trust-core sub-area). The header of every chunk lists its areas and files.
- Files are never cut mid-line. Four very large files are split into two parts, labelled `[PART 1/2, lines 1-N]`:
  apps/admin/src/main.ts, apps/creator-console/src/views.ts, services/trust-core/src/console.ts, services/trust-core/src/index.ts.
- `INDEX.md` in each folder maps every file to its chunk, so a reviewer who sees an import can find which chunk to request next.
- Verified: every file reassembles byte for byte from the chunks.

## Suggested prompt for each chunk

> You are reviewing one chunk of a larger TypeScript/SQL codebase (a trust and verification platform). Other files are in other chunks, so don't flag an import as missing just because it isn't shown here. Look for real defects: authorization or tenant-isolation gaps, injection, race conditions and transaction problems, crypto or signature-verification mistakes, error paths that fail open, data leaks in logs or responses, and logic bugs. For each finding give the file, the line or function, a concrete failure scenario, and how confident you are. Skip style comments.

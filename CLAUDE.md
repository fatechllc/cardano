# CLAUDE.md — cardano

> ## Session-start protocol (READ FIRST)
> Before working in this repo, load the shared Vladium knowledge so behaviour and
> standards are inherited, not re-derived:
> 1. **`~/Projects/tooling-kb/AGENT-README.md`** — Vladium KB session-start protocol,
>    hard rules, inbox flow, output-format rule.
> 2. **`~/Projects/tooling-kb/projects/cardano.md`** — the Vladium card for this
>    project. None exists yet; this repo is small enough that one is optional, but
>    add it if the pool becomes an active workstream.
> 3. **`README.md`** in this repo — the file format rules and the re-registration
>    procedure. Read it before touching `poolMetaData.json`.
>
> Not a web/marketing project, so `~/Projects/web-projects-handbook/` does not apply.
>
> Follow the handbook/KB rather than re-deriving. If you find a gap in the shared
> docs, fix the shared doc so the next project inherits it.

## What this is

A single-file repository holding `poolMetaData.json`, the public metadata for the
Fatech Cardano stake pool. GitHub serves it at a raw URL that the pool's on-chain
registration certificate points to. No build, no dependencies, no application code.

## Non-negotiables

- **This repo is PUBLIC** (`fatechllc/cardano`). Nothing goes in it that is not
  meant for the whole internet. No keys, no seed phrases, no internal notes, no
  contact details beyond what already ships in the metadata file.
- **Never put pool keys, wallet keys, or any secret material in this repo.** They
  live on the pool operator machine only.
- **Editing `poolMetaData.json` is not a complete change.** The registration
  certificate stores a blake2b hash of the file. A commit that changes the file
  without a follow-up on-chain re-registration breaks the pool's metadata for
  wallets and explorers. See README for the full procedure. Surface this to
  Vladimir before proposing any edit to the file.
- **Respect the size limits** (512 bytes total; ticker 3-5 chars; name 50;
  description 255; homepage 64). Exceeding them makes the metadata invalid.
- **Do not rename the file, change its path, or rewrite history on `main`.** The
  raw URL is baked into an on-chain certificate.
- Default branch is `main`. Commits: lowercase, imperative, no conventional-commit
  prefix, ending with the standard `Co-Authored-By` trailer.

## Scope

Maintenance only: correcting the metadata text when the pool's public details
change, and keeping these docs accurate. Do not add tooling, CI, node
configs, or scripts here unless Vladimir asks; operational pool tooling belongs on
the operator machine, not in a public metadata repo.

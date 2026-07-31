# cardano

Public metadata for the Fatech Cardano stake pool.

This repo exists for one reason: to serve `poolMetaData.json` at a stable public
URL that the pool's on-chain registration certificate can point to. There is no
build, no dependencies, and no application code.

## Contents

| File | Purpose |
| --- | --- |
| `poolMetaData.json` | Pool name, ticker, description, homepage. Fetched by wallets and pool explorers. |

Served from the repo's raw URL on `main`:

```
https://raw.githubusercontent.com/fatechllc/cardano/main/poolMetaData.json
```

## Format rules (enforced by the Cardano node, not by us)

- `ticker` — 3 to 5 characters
- `name` — 50 characters max
- `description` — 255 characters max
- `homepage` — 64 characters max
- whole file — 512 bytes max
- the metadata URL itself — 64 characters max

## Changing the metadata is a two-step operation

The pool registration certificate stores a **hash** of this exact file, not just
the URL. Editing `poolMetaData.json` without re-registering leaves the on-chain
hash pointing at content that no longer matches, and explorers will show the pool
as having invalid metadata.

To change anything in the file:

1. Edit and commit the file.
2. Recompute the hash:
   `cardano-cli stake-pool metadata-hash --pool-metadata-file poolMetaData.json`
   (subcommand path varies by `cardano-cli` version).
3. Submit an updated pool registration certificate carrying the new hash, from
   the machine that holds the pool keys. Keys are never stored in this repo.

Step 3 costs a transaction fee and is not reversible by editing GitHub. Do not
treat a commit here as a completed change.

## Status

Pool ticker, pool ID, and current registration state: TBD (not tracked in this
repo). The repository is public by design.

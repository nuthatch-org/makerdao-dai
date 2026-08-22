# makerdao-dai

A [nuthatch](https://github.com/nightswatchhq/nuthatch) nest: **DAI on Ethereum**.

The DAI token's transfers and approvals.

One binary, one config file, no graph-node, no gateway, no query fees.

## What it indexes

**Chain:** `mainnet`. **1 contract**, **2 tables**.

| alias | address |
|---|---|
| `c0` | `0x6b175474e89094c44da98b954eedeac495271d0f` |

## Verified

Indexed blocks **25,791,627 to 25,811,563** and sealed **82,762 events**. Every table below is generated from the vendored ABIs, and the run above is what this nest actually decoded, not an estimate.

## Read this before trusting it

- A substitute for a `makerdao` nest, which is **not buildable**: the Vat's only event is `LogNote` and it is anonymous - no topic0, the function selector sits in its slot - so a topic0-keyed decode yields zero tables. True of every core dss contract.

## Run it

```sh
nuthatch init --from https://github.com/nightswatchhq/makerdao-dai
cd makerdao-dai
nuthatch dev --dir . --backfill 50000 --seal-direct
nuthatch sql --dir . "SELECT count(*) FROM \"c0__approval\""
```

The endpoint in `nuthatch.toml` is keyless and public, so this file is publishable: a `nuthatch.toml` is pinned into the nest's content address and must never carry a credential. It is enough to follow the tip. A **backfill** wants archive depth it may not have: pass your own with `--rpc`, and check it first with `nuthatch doctor --rpc <url>`.

## Tables

```
c0__approval
c0__transfer
```

# Agent guide — Liana Litecoin

LitecoinDevKit fork of [wizardsardine/liana](https://github.com/wizardsardine/liana).
Desktop Litecoin wallet for inheritance, loss protection, and safer backups.

**Status:** Phase 0 scaffold. Daemon and GUI sources are still upstream Bitcoin Liana.
Litecoin / MWEB are not implemented. Not mainnet-ready.

Human onboarding (reading order, domain homework, first tasks): [`docs/ONBOARDING.md`](docs/ONBOARDING.md).

## Canonical docs

| Doc | Use for |
|-----|---------|
| [`docs/PLAN.md`](docs/PLAN.md) | Goals, phases, architecture, open questions |
| [`UPSTREAM.md`](UPSTREAM.md) | Fork SHA, remotes, merge conflict rule |
| [`doc/AI_POLICY.md`](doc/AI_POLICY.md) | Required AI contribution rules |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Commits, MSRV, maintainer vs external workflow |

Cursor rules under [`.cursor/rules/`](.cursor/rules/) reinforce these constraints in-session.

## Hard constraints

- Do not claim mainnet readiness or working Litecoin/MWEB features.
- Do not embed Nexus, `lndltc`, or in-process `mwebd` (GPL / wrong architecture).
- Transparent vault = Script / miniscript `older(N)`. MWEB recovery = wallet protocol
  (height-locked pre-signed txs + heir backup), **not** Script CSV on MWEB outputs.
- Three stores never merge: transparent UTXOs | MWEB coins | recovery package backup.
  Never fold HogAddr into the transparent UTXO index.
- Stay a thin, mergeable fork of upstream where practical.
- Liana Connect / SaaS and renaming `liana*` crates are out of scope for v1.

## Current work focus

Phase 1 when started: transparent Litecoin port (chain types, networks, `ltc1…`,
Electrum-LTC / litecoind). Create a `litecoin` working branch then.

Do **not** jump to MWEB sync or recovery packages (Phases 3–4) before transparent
vault dogfood (Phase 2).

## Workflow

- Prefer small, atomic, buildable commits; do not mix formatting with logic.
- Maintainer may push to `litecoin` (or `master` in Phase 0); external work and large/funds
  changes use PRs — see `CONTRIBUTING.md`.
- Human owns issues, PR bodies, and review replies (see AI policy).
- Before claiming done: build/test with Cargo; use `tests/` blackbox where relevant.
- Read `docs/PLAN.md` before large changes; update it when a phase completes.
- On upstream merges: keep this fork’s README / `docs/PLAN.md` / `UPSTREAM.md`;
  take upstream for untouched daemon/GUI until Phase 1+ diverges.

## Crate map

| Crate | Role |
|-------|------|
| `liana` | Policy, descriptors, spend / recovery, signer |
| `lianad` | Daemon: backends, DB, JSON-RPC over Unix socket |
| `liana-gui` / `liana-ui` | Iced installer + wallet UI / design system |
| `liana-connect` / `liana-business` | Hosted / business paths — not v1 LTC scope |

Build: [`doc/BUILD.md`](doc/BUILD.md) or `nix develop`. UI work: [`UI_GUIDELINES.md`](UI_GUIDELINES.md).

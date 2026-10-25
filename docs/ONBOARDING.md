# Onboarding — Liana Litecoin

Human checklist for joining this fork. Agents should start at [`AGENTS.md`](../AGENTS.md);
this page is for people (including AI-assisted contributors).

**Status:** Phase 0 scaffold. Daemon/GUI are still upstream Bitcoin Liana. Not mainnet-ready.

## Reading order

1. [`README.md`](../README.md) — product intent
2. [`docs/PLAN.md`](PLAN.md) — goals, phases, transparent vs MWEB
3. [`UPSTREAM.md`](../UPSTREAM.md) — remotes, fork SHA, merge rule
4. [`doc/AI_POLICY.md`](../doc/AI_POLICY.md) — required if you use LLMs
5. [`CONTRIBUTING.md`](../CONTRIBUTING.md) — commits, MSRV, maintainer vs external workflow
6. [`doc/USAGE.md`](../doc/USAGE.md) / [`doc/RECOVER.md`](../doc/RECOVER.md) / [`doc/API.md`](../doc/API.md) — how Liana works as a product
7. [`UI_GUIDELINES.md`](../UI_GUIDELINES.md) — only if you touch Iced UI

## Branches (this fork)

- `master` — track upstream Liana; Phase 0 docs may land here.
- `litecoin` — create when Phase 1 starts; all LTC product work goes here (same idea as
  LitecoinDevKit/bdk). Solo maintainers may push focused commits; external contributors open PRs.
  Details: [`CONTRIBUTING.md`](../CONTRIBUTING.md).

## Two ledgers (must know)

| Account | Mechanism | Recovery enforcement |
|---------|-----------|----------------------|
| Transparent vault | Liana multipath miniscript | On-chain Script `older(N)` |
| Private (MWEB) | LDK MWEB + LIP-0006 | Height-locked pre-signed txs + heir backup |

Same *features* on both; different *enforcement*. Three stores never merge: transparent UTXOs,
MWEB coins, recovery package backup. Never index HogAddr as transparent UTXOs. Never embed Nexus /
`lndltc` / in-process `mwebd`. Details: [`PLAN.md`](PLAN.md) Architecture.

## Remotes

```text
origin    https://github.com/LitecoinDevKit/liana-ltc.git
upstream  https://github.com/wizardsardine/liana.git
```

## Build and explore

1. Follow [`doc/BUILD.md`](../doc/BUILD.md) or `nix develop`.
2. Build debug: `cargo build` (binaries under `target/debug`).
3. Skim [`tests/README.md`](../tests/README.md); run a focused unit or blackbox path when you change daemon logic.
4. Mental map (re-explain in your own words after exploring):
   - Multipath descriptors: `liana/src/descriptors/`
   - Backends / poller: `lianad/src/bitcoin/`
   - Recovery RPC: `createrecovery` in `doc/API.md` → implementation
   - GUI ↔ daemon: `liana-gui/src/daemon/`

## Domain homework

Spend time on these before Phase 1 work — an LLM cannot substitute for this:

- Miniscript and relative timelocks (`older`) — why primary vs recovery works on transparent LTC
- Why MWEB stealth receives break Script multipath (see LIP-0002 and `PLAN.md`)
- LDK pin ladder (Phase 3+): [LitecoinDevKit/bdk `docs/ADOPTION.md`](https://github.com/LitecoinDevKit/bdk/blob/litecoin/docs/ADOPTION.md)
- Fork discipline: keep this repo’s README / `PLAN` / `UPSTREAM` on merges; take upstream for untouched daemon/GUI until you diverge

## Using AI here

AI tools are welcome under [`doc/AI_POLICY.md`](../doc/AI_POLICY.md):

- You must be able to explain what changed, why, and how you verified it
- Human owns issues, PR bodies, and review replies — do not paste model output into GitHub
- No autonomous agent-driven PRs; no agents as git author/co-author
- Cursor rules under [`.cursor/rules/`](../.cursor/rules/) reinforce this in-session

**Testing-led ownership is okay.** You do not have to deep-read the whole codebase before shipping. A solid loop is: you choose the work and success criteria → agent drafts → you verify with builds/tests (and skim the shipped diff for funds-touching code) → you write any PR/issue text in your own words → you can defend the change if asked.

Canonical policy text in `doc/AI_POLICY.md` still applies for contributions to this repo (and upstream expectations if you contribute there).

## First useful work (Phase 1)

When Phase 1 starts, create a `litecoin` branch. Good first slices:

1. Inventory Bitcoin assumptions (networks, dust, fees, address formats, Electrum defaults) as a tracked checklist
2. Smallest type/network alias experiment — atomic, buildable commits
3. CI / build smoke once Litecoin types exist
4. Docs clarifications in `PLAN.md` when you hit real blockers

Avoid for now: Connect/business polish, UI redesign, renaming `liana*` crates, MWEB recovery before transparent dogfood (Phases 3–4).

## Ready check

You can, without relying on a model:

1. Draw transparent vs MWEB recovery enforcement
2. Point to where descriptors and recovery txs live
3. State the current phase and a sensible next change (on `litecoin` once Phase 1 starts)
4. Restate the AI policy in your own words

Then contribute under [`CONTRIBUTING.md`](../CONTRIBUTING.md).

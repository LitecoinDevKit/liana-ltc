# AI-native forking and porting

How LitecoinDevKit maintains serious chain software when **agents draft most of the
code** and a human remains product owner, verifier, and publisher.

Roadmap for this repo: [`docs/PLAN.md`](../docs/PLAN.md). Full AI hard rails:
[`AI_POLICY.md`](AI_POLICY.md).

## Hard rails (do not soften)

These stay exactly as written. They are the simplest guard against the accountability
model drifting into “the agent shipped it”:

1. **No autonomous agent-driven pull requests** — a human chooses the work, verifies, and is responsible for the contribution.
2. **No agent as git author or co-author** — commits are human-authored.

Everything else in this playbook (thin ports, oracles, testing-led ownership, AI-drafted
comments) is subordinate to those two rails.

## Cursor rules (soft guardrails)

Project rules under `.cursor/rules/` inject short reminders into agent sessions. They are
**soft in-context guardrails**, not a technical lock — humans remain accountable.

- Keep rules short; full policy stays in this file and `AI_POLICY.md`.
- If an agent repeatedly ignores a constraint, **tighten the short rule** (or add one line
  showing the bad pattern) rather than pasting more of the playbook into always-apply rules.
- Rules are living; these docs remain the source of truth.

## Mission

We fork and port with AI as the default implementer. Humans remain accountable for
what ships. **Language fluency is optional. Verification and honesty are mandatory.**

This differs from Bitcoin Core–style AI policy, which assumes fluent authors and
AI as a side tool in a multi-reviewer culture.

## Role split

| Role | Does | Does not |
|------|------|----------|
| **Human** | Choose work and success criteria; run or designate verification; approve posts; merge/push; own mistakes | Need to hand-write every line; need professional Rust fluency |
| **Agent** | Explore, draft, refactor, propose tests and short comment/PR text | Open PRs alone; appear as commit author/co-author; invent chain semantics or mainnet claims |

## Ownership bar

Enough to ship a change:

- Explain **what** changed, **why**, and **how it was verified**
- Defend effects (networks, keys, balances, disclaimers) if asked
- For funds-adjacent paths: skim the shipped diff and record verification in the form below — prefer independent tests over “CI green”

Not required: line-by-line mastery of the whole tree or inventing idiomatic Rust without help.

**Testing-led ownership** is first-class: design cases → agent drafts → build/test → fail/fix →
human publishes.

## Thin port + external oracle

Prefer **thin ports** over rewrites:

- Alias / swap chain types, networks, fees, address formats
- Keep upstream algorithms and policy engines intact where practical
- Stay mergeable (`master` ≈ upstream; product work on `litecoin` — see [`CONTRIBUTING.md`](../CONTRIBUTING.md))

Prefer an **external oracle** over inventing truth from scratch:

- Borrow golden tests, reference-implementation vectors, and upstream/library test suites
- Example (LitecoinDevKit/bdk): keep BDK light via aliasing; verify MWEB against **mwebd / golden**
  tests — *using* those tests as oracles is not the same as embedding `mwebd` in the product
- For this repo: Phase 1 aliases Liana onto Litecoin types; Phase 3+ leans on LDK tests/vectors;
  still **never** embed Nexus / `lndltc` / in-process `mwebd` (see PLAN)

Agents draft the adapter code. Humans pick the **seam** and the **test source of truth**.

## Verification ladder

Raise the bar as risk rises:

1. Docs / PLAN honesty (no fake mainnet or mechanism parity claims)
2. Build + unit tests
3. Blackbox / regtest (see `tests/`)
4. Testnet dogfood
5. Security review / audit before signed mainnet claims

Do not skip rungs with marketing copy.

## Communication

- On this fork: human-reviewed AI drafts for issues, PRs, and comments are OK if clear and succinct
- Upstream projects may forbid AI-looking comments — follow *their* rules there
- Disclose raw pasted transcripts; ordinary edited drafts need no special label

## Mistakes

Mistakes happen. Own them, fix them, leave a clear trail. Do not hide errors or blame the model.

## Agent checklist (short)

- Obey hard rails: never open/drive PRs; never appear as git author/co-author
- Read `docs/PLAN.md` / `AGENTS.md` before large changes
- Prefer small, atomic, buildable commits
- Thin aliasing over speculative rewrites
- Point at existing tests or propose golden/reference coverage
- Help the human verify; do not claim done without a verification path
- Draft short GitHub text for human edit — do not post autonomously

## Human checklist (short)

- Choose the next phase-aligned slice
- Review/approve anything public
- Update PLAN when a phase gate moves
- Own and fix breakage
- Keep hard rails intact (no autonomous PRs; no agent as author/co-author)

### Verification record (mandatory for funds-adjacent work)

For any change that touches **keys, balances, networks, or signing** (descriptors, spend,
recovery, broadcast, coin index, MWEB packages), write down before you merge/push:

| Field | Required content |
|-------|------------------|
| **Command(s)** | Exact test or build invocation(s) you ran (or the blackbox path) |
| **Expected outcome** | What success looks like (pass, specific log, balance/address check) |
| **Oracle** | Which source of truth you consulted (e.g. crate unit tests, `tests/` blackbox, LDK suite, mwebd/golden vectors, manual testnet step) — or `n/a (docs-only)` |

“CI is green” alone is not enough for these paths. Put the record in the commit body, PR
description, or a short note next to the change so the trail survives.

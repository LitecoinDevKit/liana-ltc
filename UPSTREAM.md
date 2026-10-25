# Upstream

This repository is a fork of [wizardsardine/liana](https://github.com/wizardsardine/liana).

## Fork point

| Field | Value |
|-------|-------|
| Upstream remote | `https://github.com/wizardsardine/liana.git` |
| Fork created from | `master` |
| Upstream commit at fork | `7678de4a87db95d5c0557d58afbe85e9bd9a2e0d` |
| Upstream tip message | `Merge #2379: deps: bump electrum-client to 0.24.2` |

Confirm locally:

```bash
git rev-parse HEAD   # at first LitecoinDevKit commit parent / initial clone tip
git log -1 --oneline upstream/master
```

## Remotes

```text
origin    https://github.com/LitecoinDevKit/liana-ltc.git
upstream  https://github.com/wizardsardine/liana.git
```

## Merging upstream

Prefer regular merges (not rewrite history of published `master`):

```bash
git fetch upstream
git checkout master   # or litecoin once that branch exists
git merge upstream/master
```

Resolve conflicts with the rule: keep LitecoinDevKit README / `docs/PLAN.md` / `UPSTREAM.md`
overrides; take upstream for untouched daemon/GUI code until Phase 1+ ports diverge.

After a successful merge, update the “Fork point” table above if you want the doc to track the
last integrated upstream SHA (optional; `git merge-base` remains authoritative).

## License

Upstream and this fork use the **BSD 3-Clause** licence (`LICENCE`). Retain copyright notices.
Do not imply endorsement by Wizardsardine or the Liana developers (BSD clause 3).

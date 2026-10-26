# Contributing to Liana

Anyone is welcome to contribute to Liana regardless of any arbitrary criterion. Contribution are
only judged based on their technical relevance and quality.

Note that the development of Bitcoin software requires a high level of rigor, so it could take some
time (and backs and forths) to polish a contribution before it's ready for merge.

If you use AI tools while contributing, read and follow the
[AI policy](doc/AI_POLICY.md) and the [AI-native forking playbook](doc/AI_NATIVE_FORKING.md).
Contributors are responsible for verifying and explaining their own work.

New to this fork? See [docs/ONBOARDING.md](docs/ONBOARDING.md) for a short getting-started
checklist (roadmap context, build, domain background, AI workflow).


# LitecoinDevKit maintainer workflow

This fork is often a **solo** line of work (same pattern as LitecoinDevKit/bdk’s `litecoin`
branch). Upstream’s PR-for-everything rule below still applies to **external** contributors and to
large or funds-adjacent changes. Maintainers need not open a self-PR for every docs or small fix.

| Branch | Role |
|--------|------|
| `master` | Stay close to `upstream/master` (wizardsardine/liana); prefer regular merges — see [UPSTREAM.md](UPSTREAM.md) |
| `litecoin` | Litecoin product work (Phase 1+). Create when the transparent port starts ([docs/PLAN.md](docs/PLAN.md)) |

**Day to day (maintainer):** push focused, atomic, buildable commits to `litecoin` (or `master`
during Phase 0 scaffold). Prefer commit messages that explain *why*.

**Use a pull request when:** someone else may review; you want CI/Actions as a gate; the change is
large or touches funds/descriptor/spend paths; or you want a durable review artifact.

**Still required either way:** hygienic commits, rustfmt, tests for new features, and the
[AI policy](doc/AI_POLICY.md) / [AI-native forking](doc/AI_NATIVE_FORKING.md)
(human-reviewed AI drafts OK; thin ports + external oracles; no autonomous agent-driven PRs).
Mistakes happen — own them and fix them.


## Communication

Most of the communication is done on GitHub or on [our Discord](https://discord.gg/9rAqZHwkv6).

If you plan to contribute a non-trivial change, consider discussing it on Discord or in a
Github issue before going forward with the implementation.


## Looking for contributions

If you are looking for first time contributions, you can `git grep` for `FIXME`s and `TODO`s
as well as checking out the [good first issues](https://github.com/wizardsardine/liana/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)
on the issue tracker.


# Workflow (external contributors)

External contributors use the "contributor workflow": patch proposals via **pull requests** (PRs).
This facilitates social contribution, easy testing and peer review. Maintainers: see
**LitecoinDevKit maintainer workflow** above.

In general, [commits should be atomic](https://en.wikipedia.org/wiki/Atomic_commit#Atomic_commit_convention)
and diffs should be easy to read. For this reason, do not mix any formatting
fixes or code moves with actual code changes.
Make sure each individual commit is hygienic: that it builds successfully
on its own without warnings, errors, regressions, or test failures.

Commit messages should be verbose by default consisting of a short subject line,
a blank line and detailed explanatory text as separate paragraph(s), unless the
title alone is self-explanatory. Commit messages should be helpful to people
reading your code in the future, so explain the reasoning for your decisions. For
more guidelines about writing commit messages, see this [blog post](https://cbea.ms/git-commit/).

If your pull request contains fixup commits (commits that change the same line of code repeatedly) or too fine-grained
commits, you may be asked to [squash](https://git-scm.com/docs/git-rebase#_interactive_mode) your commits
before it will be merged.

Patchsets should always be focused. For example, a pull request could add a
feature, fix a bug, or refactor code; but not a mixture. Please also avoid super
pull requests which attempt to do too much, are overly large, or overly complex
as this makes review difficult. Instead, prefer opening different focused pull requests.

Anyone may participate in peer review which is expressed by comments in the pull
request. Typically reviewers will review the code for obvious errors, as well as
test out the patch set and opine on the technical merits of the patch. PR should
be reviewed first on the conceptual level before focusing on code style or grammar
fixes.

Any new contributed feature must come with tests. Preferably both an integration/functional tests
demonstrating its usage in a blackbox manner (for instance calling an RPC command under different
conditions), as well as unit tests exercising specific parts of the logic (for instance a database
query).


# Code

## Minimum Supported Rust Version

`lianad` should always compile and pass tests using **Rust 1.63**. The rationale behind this is
support something reasonable, and preferably supported by all of:
- [Guix](https://guix.gnu.org/)
- Popular distributions' packages (especially Debian which is the most conservative)
- [Mrustc](https://github.com/thepowersgang/mrustc)

## Style

To avoid endless bikeshedding, just use [`rustfmt`](https://github.com/rust-lang/rustfmt).

[Clippy](https://github.com/rust-lang/rust-clippy) is also often your friend.

# AI Policy

Using AI (i.e. LLMs) as tools for coding is welcome, provided that such use adheres
to the following policy, adds value, and does not waste the time of other
contributors.

A high bar is held for all contributions to this project.

**AI-native forking / porting playbook** (thin ports, external oracles, role split,
mandatory verification records for funds-adjacent work):
[`AI_NATIVE_FORKING.md`](AI_NATIVE_FORKING.md).

**Hard rails (do not soften):** no autonomous agent-driven PRs; no agent as git author or
co-author. These keep accountability from drifting.

## Comments and review replies (this fork)

On **LitecoinDevKit/liana-ltc**, AI may help draft GitHub comments, issue text, PR
bodies, and review replies when a **human** edits or approves them before posting.
The goal is clear, succinct communication — not autonomous chatter.

The human who posts remains responsible for accuracy and tone. Do not paste long,
unreviewed model output. Prefer short drafts the human has read.

**Upstream note:** [Bitcoin Core’s AI policy][bitcoin core's ai policy] (and
wizardsardine/liana if they adopt it) expects comments written by humans and may
moderate AI-looking comments. When contributing **there**, follow that project’s
rules, not this fork’s looser comment practice.

## Pull requests and authorship

If you are opening an issue, you should be able to describe the problem (with or
without an AI draft you have reviewed).

You should only open a pull request if you (the human behind the LLM):

- can **direct, verify, and explain** the change (Rust fluency is not required on this fork)
- can defend what changed, why, and how it was verified — testing-led ownership and
  thin-port + external-oracle verification are first-class; see
  [`AI_NATIVE_FORKING.md`](AI_NATIVE_FORKING.md) and `docs/ONBOARDING.md`
- understand the effect of the suggested changes (networks, keys, funds paths, disclaimers)

You must also be able to explain the pull request changes. AI may help draft the
PR body or replies; the human must review before posting and must be able to
answer follow-ups without pasting unreviewed model output.

This project requires a human author in the loop who owns the work produced by
AI. **Pull requests should not be opened or driven by autonomous agents**. A human
author must choose the work, verify the change, and be responsible for the
contribution. Do not include agents as authors or co-authors of your commits for
these reasons. Pull requests that appear in violation of this can be closed without
notice.

If you wish to include raw context from an interaction with AI in your comments, it must
be disclosed as such. It must be accompanied by human commentary explaining the
relevance and implications of the context.

## Mistakes

Mistakes happen — with or without AI. That is okay. Own them, fix them, and leave a
clear trail (commit, comment, or follow-up PR). Do not hide errors or blame the
tooling; do not leave known breakage for someone else to discover.

Questions or proposed changes to this policy can be discussed in a GitHub issue.

This policy was adapted from [Bitcoin Core's AI policy], then adjusted for
LitecoinDevKit’s AI-native forking workflow (see [`AI_NATIVE_FORKING.md`](AI_NATIVE_FORKING.md):
human-reviewed AI drafts; testing-led ownership; thin ports + external oracles;
own-and-fix mistakes).

[bitcoin core's ai policy]: https://github.com/bitcoin/bitcoin/blob/f5d7cc66ecba075790e09b2933c782b218fa558f/doc/AI_POLICY.md

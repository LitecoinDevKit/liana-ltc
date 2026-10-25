<div align="center">
  <a href="https://github.com/LitecoinDevKit/liana-ltc" target="_blank">
    <img src="liana-ui/static/logos/liana-app-icon.svg" width="140px" />
  </a>

# Liana Litecoin

*The missing safety net for your litecoins.*

**Early scaffold / planning — not mainnet-ready. Litecoin and MWEB support are not implemented yet.**

</div>

## About

**Liana Litecoin** (short: **Liana-LTC**) is a desktop Litecoin wallet forked from
[Liana](https://github.com/wizardsardine/liana) by [Wizardsardine](https://wizardsardine.com/liana).
It targets **inheritance**, **loss protection**, and **safer backups** on Litecoin.

Like upstream Liana, you have a **primary spending path** (always accessible) and one or more
**recovery paths** (available after a period of inactivity). Either path may be multisig.

### Transparent vault (planned)

On the transparent Litecoin chain, recovery will use the same model as upstream Liana:
timelocks enforced on-chain by Script / miniscript (`older(N)` relative locktime). Primary keys can
always spend; recovery keys unlock after inactivity.

### Private Litecoin / MWEB (planned)

[MWEB](https://github.com/litecoin-project/lips/blob/master/lip-0002.mediawiki) payments on Litecoin
are **non-interactive** (stealth addresses). MWEB outputs do not carry Script multipath policies, so
recovery will **not** use Script CSV on Private Litecoin.

Planned MWEB recovery delivers the **same user-facing features** (primary always spends; heirs
recover after a delay; staged paths / multisig) via a **wallet protocol**: after each receive, the
wallet prepares height-locked pre-signed recovery transactions (`kernel.lock_height`). Same
*experience*, different *enforcement* than the transparent vault.

Do not read this README as claiming working MWEB inheritance today — see [`docs/PLAN.md`](docs/PLAN.md).

### Ecosystem

- Built on **[LitecoinDevKit](https://github.com/LitecoinDevKit)** (LDK) for Litecoin / MWEB library work
- **Nexus** (Litecoin Foundation mobile wallet) is an address/tx **interop peer** only — this project
  does **not** embed Nexus, `lndltc`, or `mwebd`
- Adoption / pin ladder for LDK: [`LitecoinDevKit/bdk` docs/ADOPTION.md](https://github.com/LitecoinDevKit/bdk/blob/litecoin/docs/ADOPTION.md)

## Status

| Area | Status |
|------|--------|
| Repo fork + planning docs | Done (this tree) |
| Litecoin transparent port | Not started |
| MWEB sync / spend | Not started |
| MWEB recovery packages | Not started |
| Releases / mainnet | Not ready |

Living roadmap: **[`docs/PLAN.md`](docs/PLAN.md)**. Upstream merge notes: [`UPSTREAM.md`](UPSTREAM.md).

## Usage

Upstream Liana install / try docs still describe **Bitcoin** (`doc/USAGE.md`, `doc/TRY.md`). They
are retained for reference until the Litecoin port lands. Do not use this fork with real funds yet.

## Hacking on Liana Litecoin

This repository is hosted at [LitecoinDevKit/liana-ltc](https://github.com/LitecoinDevKit/liana-ltc).
Contributions welcome — see [`CONTRIBUTING.md`](CONTRIBUTING.md) (upstream guidelines apply until we
add Litecoin-specific notes).

Layout matches upstream:

#### Daemon (`liana`)

Core wallet logic: Rust library + UNIX daemon with JSON-RPC over a Unix domain socket.
See the [`liana`](liana) folder.

#### GUI (`liana-gui`)

Installer + graphical UI (via [`iced`](https://github.com/iced-rs/iced/)).
See the [`liana-gui`](liana-gui) folder.

Daemon and GUI sources are **unchanged from upstream** in this scaffold pass. A `litecoin` working
branch is planned for Phase 1 (see [`docs/PLAN.md`](docs/PLAN.md)).

## Security

See [`SECURITY.md`](SECURITY.md) for vulnerability reporting. Treat this fork as experimental until
a signed release says otherwise.

## License and attribution

Released under the BSD 3-Clause Licence. See the [LICENCE](LICENCE) file.

This project is a fork of [wizardsardine/liana](https://github.com/wizardsardine/liana).
It is **not affiliated with, endorsed by, or sponsored by** Wizardsardine or the Liana developers.
“Liana” is used to acknowledge upstream; product branding may evolve (see open questions in the plan).

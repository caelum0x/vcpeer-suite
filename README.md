# VCPeer

VCPeer is a free, open-source suite of self-hosted communication tools:
video calls, large-file sending, scheduling/booking, and multistream
live broadcasting. It used to run as a paid hosted service at
vcpeer.com; as of October 2026 it's **not hosted by us anymore** — it's
100% free, open source, and meant to be self-hosted by you.

This repo is a monorepo bringing together the four previously separate
VCPeer repositories, each kept in its own folder under `apps/` with its
full original git history preserved (via `git subtree`):

| App | Folder | What it is | Base project | License |
|---|---|---|---|---|
| **VCPeer Call** | [`apps/call`](apps/call) | Peer-to-peer video calls, screen share, chat, recording, live captions/transcripts, scheduler | Fork of [MiroTalk P2P](https://github.com/miroslavpejic85/mirotalk) | AGPL-3.0 |
| **VCPeer Send** | [`apps/share`](apps/share) | WeTransfer-style large-file sending: upload, get a link, set expiry/password, email the recipient | Fork of [Pingvin Share X](https://github.com/smp46/pingvin-share-x) | BSD-2-Clause |
| **VCPeer Book** | [`apps/book`](apps/book) | Scheduling/booking pages, calendar sync, Jitsi video links per booking | Fork of [Cal.com / cal.diy](https://github.com/calcom/cal.diy) | MIT |
| **VCPeer Live** | [`apps/live`](apps/live) | Free multistream: go live once, broadcast to Twitch/Kick/YouTube at the same time, plus a watch page with chat | Built on [Owncast](https://owncast.online/) + [MediaMTX](https://github.com/bluenviron/mediamtx) | MIT |

Each app is a complete, independently deployable product with its own
`README.md`, `LICENSE`, `.env.example`, and Docker/deploy setup inside
its folder — this repo doesn't glue them together into one process, it
just gives you one place to find, clone, and run all of them.

## Why this repo exists

All four apps used to live in separate GitHub repos
(`vcpeer-mirotalk`, `vcpeer-share`, `vcpeer-book`, `vcpeer-live`). They've
been merged here into one monorepo so there's a single place to find
the whole VCPeer suite, with each app's commit history preserved under
its own `apps/<name>/` subtree. The original repos still exist on
GitHub (for history/reference) but this repo is now the canonical,
actively-linked home for VCPeer.

## Self-hosting

Each app is independent — you can run just the one you want, or all
four. Start with the app's own README:

- [`apps/call/README.md`](apps/call/README.md) — video calls (Node.js/Express, Docker or `npm start`)
- [`apps/share/README.md`](apps/share/README.md) — file sending (Next.js + NestJS, Docker Compose)
- [`apps/book/README.md`](apps/book/README.md) — booking (Next.js, Docker Compose + Postgres)
- [`apps/live/README.md`](apps/live/README.md) — live multistream (Docker Compose: Owncast + MediaMTX + a small control app)

Every app ships a `.env.example` (or `config.example.yaml` for Send) —
copy it to `.env`, fill in your own values, and never commit the real
file. None of these apps require any VCPeer-operated service to run:
no license server, no phone-home, no required third-party SaaS. SMTP,
S3/object storage, and OAuth providers are all optional and
bring-your-own.

## License

This repository bundles multiple independent applications under
**different open-source licenses** — there is no single top-level
license for the whole repo. Each app keeps its own license in its own
folder:

- `apps/call/LICENSE` — AGPL-3.0 (inherited from MiroTalk)
- `apps/share/LICENSE` — BSD-2-Clause (inherited from Pingvin Share X)
- `apps/book/LICENSE` — MIT
- `apps/live/LICENSE` — MIT

If you redistribute or deploy any one app, follow that app's own
license, not a license from a different folder.

## Status

VCPeer is no longer operated as a paid, hosted product. There's no
roadmap commitment, no SLA, no support contract — it's shipped as-is
for anyone who wants to self-host it. Issues and PRs against any `apps/*`
folder are welcome.

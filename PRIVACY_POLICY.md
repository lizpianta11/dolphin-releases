# Dolphin — Privacy Policy (Beta)

_Last updated: 2026-06-25 · Applies to: Dolphin macOS desktop app (beta)_

Dolphin is built to respect your privacy. In plain terms: **Dolphin is local-first
and does not send your network data anywhere.**

## What Dolphin does
- Dolphin **passively observes network packet *metadata*** for networks and
  devices on your local network — protocols, addresses/ports, sizes, timing, and
  the like.
- Dolphin **does not block, filter, or modify traffic.** It only watches and
  explains. It is a monitoring/analysis tool, not a firewall.

## Local-first / no cloud
- **Dolphin does not send captured packet data to the cloud.** Analysis happens
  on your Mac.
- **OTORO** (the built-in AI helper) runs **locally** via a bundled Ollama
  runtime and a local model — prompts and answers are generated on your machine
  and are **not** sent to any external server.
- **Raw packet payloads are not collected or sent by default.** Dolphin works on
  metadata; raw payloads are only ever included if you explicitly enable a
  raw/opt-in mode, and even then they are used locally.
- **No cloud account** is connected in this beta (the in-app "Local Profile" is
  stored only on your Mac).
- **No telemetry** is collected in this beta — Dolphin does not phone home with
  usage data, analytics, or crash reports.

## Authorized use only
You must only use Dolphin to monitor **networks and devices that you own or are
explicitly authorized to monitor.** Capturing traffic on networks you do not own
or have permission to analyze may be illegal in your jurisdiction. You are
responsible for using Dolphin lawfully.

## What may be stored locally on your Mac
Everything below stays on your device:
- **Session metadata** — saved capture sessions you create.
- **Packet metadata** — the observed facts for the current/saved session.
- **Reports / exports** — JSON, HTML, or PDF files you generate (saved where you
  choose, typically Downloads).
- **Local profile name** — the optional display name you set under "Local
  Profile" (no email, no password, no account).
- **Local OTORO / audit history** — your OTORO conversations and local audit log
  entries, kept on-device.
- **OTORO model** — downloaded once and stored locally by the Ollama runtime.

## How to delete your local data
- **Reports/exports:** delete the files you exported (e.g. from Downloads).
- **Local profile:** open **Local Profile → Clear local profile**.
- **Sessions / OTORO history / audit logs:** these live in the app's local
  storage; removing the app clears the app-managed local data, or clear items
  in-app where offered.
- **Full removal:** quit Dolphin, delete `/Applications/Dolphin.app`, and remove
  the capture helper (see `docs/CLEAN_MAC_TEST.md` → Uninstall). The locally
  downloaded OTORO model is managed by Ollama's own storage if you installed
  Ollama separately.

## Changes to this policy
This is a beta document and may change as Dolphin evolves (for example, if
optional cloud features are ever added, they would be clearly described and
opt-in). The "Last updated" date reflects the current version.

## Contact / support
Support contact: <support@orsosolutions.com>

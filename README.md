# Dolphin (macOS Beta)

Dolphin is a **local-first Wi-Fi / network monitoring and analysis** app. It
passively watches network **packet metadata** on networks you own or are
authorized to monitor, and a built-in local AI (**OTORO**) explains what it sees
in plain language — all on your Mac, nothing sent to the cloud.

## What Dolphin is NOT
- ❌ **Not antivirus** and **not EDR** — it doesn't scan files or remove malware.
- ❌ **Not a firewall / blocker** — it **observes only**; it never blocks, filters,
  or modifies traffic.
- ❌ **Not a guarantee of security** — it surfaces evidence from observed metadata;
  it can't prove a device is safe or compromised.
- ❌ Not a cloud service — no account, no server, no telemetry in this beta.

## System requirements
- **macOS 13 (Ventura) or newer**
- **Apple Silicon or Intel** (the app is a universal binary)
- **Internet on first run** — OTORO downloads its local model the first time
- **Admin permission once** — the first capture installs a small helper that lets
  Dolphin read packets

## Install
1. **Download** `Dolphin-production.dmg`.
2. **Open** the DMG (double-click).
3. **Drag Dolphin to Applications.**
4. **Launch** `Dolphin` from Applications. A one-time "downloaded from the
   Internet" prompt is normal — click **Open**. (Dolphin is signed with a
   Developer ID and notarized by Apple, so Gatekeeper allows it.)
5. **Allow the admin/helper prompt** the first time you start monitoring.

## First-run expectations
- **OTORO model setup:** the first time you open OTORO, it downloads its local
  model via the bundled Ollama (needs internet) and then shows **"OTORO Ready."**
- **Capture permission:** the first capture asks for an **admin password** to
  install the monitoring helper.
- **Monitoring is metadata-only:** Dolphin watches protocols/addresses/ports/
  sizes/timing — not your message contents. It does **not** block anything.

## Quick test checklist (after install)
- [ ] Start monitoring → header shows **"Monitoring active"**
- [ ] **Wi-Fi Check** shows live packets
- [ ] Pause → select a packet → **Explain this packet** opens an in-place
      explanation pinned to that packet (and **Copy** shows "Copied")
- [ ] **Reports** → export **JSON**, **HTML**, and **PDF**
- [ ] OTORO answers a question locally (e.g. "should I worry about it?")

## Uninstall
1. **Quit Dolphin.**
2. Delete **`/Applications/Dolphin.app`** (drag to Trash).
3. Remove the capture helper (root LaunchDaemon) — exact commands are in
   `docs/CLEAN_MAC_TEST.md` → **Uninstall**:
   ```
   sudo launchctl bootout system/com.dolphin.protection 2>/dev/null || true
   sudo rm -f /Library/LaunchDaemons/com.dolphin.protection.plist
   ```
4. **Local data:** delete any reports/exports you saved (e.g. Downloads), and use
   **Local Profile → Clear local profile**. See `docs/PRIVACY_POLICY.md` for the
   full list of what's stored locally and how to remove it. (The OTORO model is
   managed by Ollama's own local storage.)

## Known beta limitations
- **macOS only** — Windows is future work.
- **No auto-update yet** — beta updates mean re-downloading the DMG for now.
- **No cloud account / billing** — Dolphin is local-first; "Local Profile" is
  on-device only.
- **OTORO requires first-run setup** — the local model downloads once (needs
  internet) before OTORO can answer.
- **Helper install will be improved** — capture currently uses a manual signed
  root helper (works on a clean Mac); a smoother install/uninstall is planned.
- **Privacy & authorized use:** Dolphin is metadata-only and local-first; only
  monitor networks/devices you own or are authorized to monitor. See
  `docs/PRIVACY_POLICY.md`.

## Support / feedback
Beta feedback: <support@orsosolutions.com>

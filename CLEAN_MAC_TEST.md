# Dolphin — Clean-Mac Test (final release acceptance)

Goal: prove the **notarized** `Dolphin-production.dmg` installs and works on a Mac
that **never built Dolphin** — the last gate before public download.

> ⚠️ Gatekeeper only enforces on **downloaded** files (the quarantine flag).
> Always get the DMG onto the test Mac via a real **download or AirDrop**, not
> `scp`/Terminal copy, or you'll get a false pass.

## Artifact under test
- **DMG:** `~/Desktop/Dolphin-Release/Dolphin-production-20260625.dmg` (36 MB, universal x86_64+arm64)
- **SHA-256:** `5219bcf33bad0df34bbe40b452122008f927df3dd9e230cbfba28db938fcb284`
- **Signed:** Developer ID Application: Orso IT Solutions LLC (QG22ZXUQB3)
- **Notarization:** `551599d5-49d9-435b-aba3-44b4cce04437` → Accepted; stapled
- On the build Mac it already passes: `spctl -a` → "accepted, source=Notarized Developer ID".

## Test environment
- A **second Mac** (Intel and/or Apple Silicon — the DMG is universal), **or** a brand-new macOS user account that never built Dolphin.
- macOS 13.0 or newer (app `minimumSystemVersion`).
- Internet on first run (OTORO pulls its model — see step 8).

## Steps

### 1. Get the DMG onto the test Mac (quarantined)
Download it via a browser, or AirDrop it. Optionally confirm the quarantine flag is set:
```
xattr -p com.apple.quarantine ~/Downloads/Dolphin-production-20260625.dmg   # should print a value
shasum -a 256 ~/Downloads/Dolphin-production-20260625.dmg
# expect: 5219bcf33bad0df34bbe40b452122008f927df3dd9e230cbfba28db938fcb284
```

### 2. Open the DMG
- Double-click → it should mount with **no Gatekeeper warning**.

### 3. Install
- Drag **Dolphin** to **Applications**.

### 4. Launch + confirm Gatekeeper allows it
- Open `/Applications/Dolphin.app`. A one-time "downloaded from the Internet — are you sure?" prompt is normal; click **Open**. There must be **no** "unidentified developer / cannot be opened" block.
- Optional terminal confirmation on the test Mac:
```
spctl -a -vvv /Applications/Dolphin.app     # expect: accepted, source=Notarized Developer ID
codesign --verify --deep --strict --verbose=2 /Applications/Dolphin.app   # expect: valid on disk
```

### 5. Capture helper / admin prompt
- Click **Start Monitoring**. Expect **one** admin authorization to install the capture helper (`com.dolphin.protection`).
- Capture should then start — **or** fail with a *clear* message (which would flag that the signed SMAppService/helper install needs more work). It must not fail silently.

### 6. Confirm Monitoring starts
- Header shows **"Monitoring active"**; Home shows live Wi-Fi capture (interface, rising packet count). No "Protection" wording anywhere.

### 7. Packet explanation works
- Wi-Fi Check → **Pause** → select a packet → **Explain this packet**.
- Confirm the in-place **"Explanation for selected packet"** panel opens (no jump to an empty OTORO chat), pinned to that exact packet (source/dest/protocol/ports/size), with cautious evidence-first wording and the "metadata only · no blocking" note.
- Click **Copy** → shows **"Copied"**.

### 8. OTORO first-run model setup
- Open **OTORO**. On a clean machine it pulls `raymondpianta/otoro-mini` via the bundled Ollama (needs network) with visible progress, then reaches **"OTORO Ready"**.
- Ask "should I worry about it?" on a tracked device → cautious, evidence-first answer; **nothing is sent to the cloud** (local 127.0.0.1 only).

### 9. Exports
- **Reports** → Export **JSON**, **HTML**, **PDF** (PDF via print). Each should write a real file (Downloads) that opens. **No CSV option** (correct).

### 10. Beginner / Pro
- Toggle top-right modes: Beginner shows the plain device summary + collapsed exact facts; Pro shows the full observed-facts grid.

## Uninstall notes
1. Quit Dolphin.
2. Remove the app: drag `/Applications/Dolphin.app` to Trash.
3. Remove the capture helper (installed as a root LaunchDaemon):
```
sudo launchctl bootout system/com.dolphin.protection 2>/dev/null || true
sudo rm -f /Library/LaunchDaemons/com.dolphin.protection.plist
```
4. (Optional) Local data is per-user app storage + the local Ollama model; removing the app stops all monitoring. OTORO's model lives under Ollama's own store if Ollama was already installed separately.

## Pass criteria
All of: DMG opens with no warning · app launches (no Gatekeeper block) · `spctl` = Notarized Developer ID · helper prompt → capture starts (or clear failure) · Monitoring active · packet Explain works in place · Copy shows "Copied" · OTORO model pulls + Ready · JSON/HTML/PDF export · Beginner/Pro both render · uninstall removes app + daemon.

## Status
**BLOCKED / PENDING** — must be run by Raymond on another Mac (or fresh user) via a real download. Update `RELEASE_CHECKLIST.md` → "Gatekeeper test on a clean Mac" to `done` only after this passes.

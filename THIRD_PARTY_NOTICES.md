# Third-Party Notices

Dolphin includes third-party software. The components below retain their own
licenses and copyrights. This file records what Dolphin bundles or relies on and
under what terms.

---

## Ollama

- **Component:** Ollama (local large-language-model runtime / CLI + server)
- **Version bundled:** 0.30.9
- **Source:** Official Ollama project — <https://github.com/ollama/ollama> / <https://ollama.com>
- **License:** MIT License
- **Architecture:** universal macOS binary (`x86_64` + `arm64`)
- **How Dolphin uses it:** Dolphin bundles the Ollama executable solely to run
  **OTORO local-only inference** on the user's machine (`127.0.0.1:11434`). No
  packet data, prompts, or model traffic leave the device — OTORO never makes
  cloud calls. The bundled binary is embedded into `Dolphin.app` and code-signed
  with Dolphin's Developer ID during production packaging.
- **Integrity (bundled build):** SHA-256
  `b47729f7ee7596cb95419f413ef6f2e9ddd7309ec038c89c4815d52c340c24bf`
  (the production build verifies this checksum before embedding —
  `dolphin/apps/desktop/scripts/package-macos-production.sh`).

### MIT License (Ollama)

```
MIT License

Copyright (c) Ollama

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

> Note: the copyright line above reflects the Ollama project's MIT license as
> published in the official repository. Verify the exact upstream `LICENSE` text
> for the bundled version before public release if precise attribution wording is
> required.

---

## Model: raymondpianta/otoro-mini

- **Component:** OTORO local model, pulled at runtime via Ollama.
- **Distribution:** not bundled in the app; downloaded on first run.
- **License/terms:** tracked separately (see `RELEASE_CHECKLIST.md` →
  "Model license + size tracking").

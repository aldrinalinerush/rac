# RAC — Rapid Assist Console

A fast, offline-first call-assist console for fraud & risk phone work: ready-to-say lines for
every call scenario (openings, verification, de-escalation, holds, voicemail, email hand-off,
and more), organized in call order, fully editable in the app.

**Author:** John Aldrine Ilao · [LinkedIn](https://www.linkedin.com/in/johnaldrineilao/) · johnaldrineilao@gmail.com

---

## Quick start

Open **`index.html`** in any modern browser. That's it — no install, no server, no build step.
Works fully offline.

## File map

| Path | Purpose |
|---|---|
| `index.html` | The entire app — HTML, CSS, and JS in one self-contained file (by design: guarantees identical rendering everywhere and zero external dependencies). |
| `assets/` | Logo kit (primary icon, mono white/dark, horizontal lockups). Not required by the app — the icon is embedded inline. |
| `README.md` | This file. |

Inside `index.html`, the script is organized in numbered sections (CONFIG → DATA → STORE →
HELPERS → FEATURES → VIEWS → BACKUP → CONTROLS → INIT) with a data-model map in the header
comment. To change spiel content, either use the in-app editor (hover any card → ✎ Edit) or
edit the `SEED` array in section 2.

## How data works

- Everything you change (categories, sections, lines, saved list, order, theme, sidebar width)
  saves **instantly and automatically** to the browser's localStorage on that device.
- Data is **per browser, per device**. Two people using the same URL each get their own
  completely separate copy — no accounts, no login, no interference.
- **Export / Import (header buttons):** Export downloads a dated `rac-backup-YYYY-MM-DD.json`
  containing everything. Import restores it exactly. Use it to (a) back up your work, and
  (b) move your setup between devices — e.g. Export on your laptop, Import on your work PC.
- If storage is unavailable (strict private mode), the app still runs in memory and tells you
  changes won't persist. Corrupted data can never crash the app — it recovers to defaults.

> **Moving from local file to the deployed site:** the browser treats them as different
> origins, so your local edits don't transfer automatically. Export locally → open the
> deployed URL → Import. Two clicks, done.

## Deploying it free (so you can access it anywhere)

The app is a static site — any free static host works. Three good options:

**Netlify Drop (easiest, ~30 seconds, no account tooling):**
1. Go to `app.netlify.com/drop` (free account).
2. Drag this whole folder onto the page.
3. You get a URL like `your-name.netlify.app`. Share it, bookmark it, open it on your phone.

**GitHub Pages (most established domain):**
1. Create a free GitHub account → new repository → upload `index.html` (and `assets/` if you like).
2. Repository Settings → Pages → Source: `main` branch → Save.
3. Your app is at `yourusername.github.io/repositoryname`.

**Firebase Hosting (Google domain — useful if your network favors Google):**
1. Install Node.js, then `npm install -g firebase-tools`.
2. `firebase login` → `firebase init hosting` (choose this folder as public dir, single-page: No).
3. `firebase deploy`. Your app is at `yourproject.web.app`.

After deploying, updating the app = re-uploading the new `index.html`. Nobody's saved data is
affected by updates (data lives in each visitor's browser, not in the files).

## Tech notes (for developers)

- Zero dependencies, zero network calls, no framework, no build. ~65 KB single file.
- System font stack; animations limited to GPU-friendly `transform`/`opacity`.
- State is one JSON model persisted under the key `rac_v5`, with a lightweight migration
  system (`mig[]`) so shipping new default content never overwrites user data.
- Custom modal system (no native `alert`/`confirm`/`prompt`), undo snackbar for all deletions,
  FLIP-animated drag-and-drop, hash-free routing (view state persisted in the model).

© 2026 John Aldrine Ilao. All rights reserved.

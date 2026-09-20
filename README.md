# U9 Playbook — v11 (local, not deployed)

Single-file web app (`index.html`) + service worker for offline use. No build step, no runtime dependencies.

## Run locally
    cd <this folder>
    python3 -m http.server 8080      # or any static server
    open http://localhost:8080/

Service worker + "Add to Home Screen" require https or localhost. Data is stored in this browser's localStorage only.

## Tests (dev only; jsdom is not shipped with the app)
    cd tests && npm init -y && npm i jsdom@24
    node app.test.js      # 84 headless interaction checks (boots the real app)
    node lint_refs.js     # undefined-function / missing-element regression guard
    node audit2.js        # run-play geometry audit (595 plays, expects 0 issues)
    node audit3.js        # whole-library structural audit (2,000 plays, expects 0 issues)

## Deploy (manual — nothing here publishes automatically)
Upload the six files at the top level of this folder to the GitHub Pages repo root, replacing the old ones.
The service-worker cache is `playbook-v11`; installed devices pick up the update on their next online open and are
offered a reload — never forced while a timer is running.

## Storage keys (all localStorage)
u9meta (schema version 1) · u9squad (roster) · u9game · u9ours · u9board · u9timer · u9heroimg · u9roster (legacy, auto-migrated)
Backups: Team → Download backup / Restore (merge | replace). Replace keeps an Undo snapshot in u9backup_prev.

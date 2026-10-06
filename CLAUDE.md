# Les Games

A clean, cartoony launcher page for Matt's hosted web games. It works like a bookmark page: tap a tile, the game opens.
Matt is not a developer. Explain everything in plain language and give exact commands, one at a time.

## Stack
- One page: index.html with its CSS and JavaScript inside. No framework, no build step, no npm packages.
- Extra files: manifest.webmanifest and icons/ for Add to Home Screen.
- Font: Fredoka from Google Fonts. Icons: inline SVG drawn in the page.
- Hosting: private GitHub repo `les-games` -> Vercel auto-deploys every push to main (no build command).

## Running locally (pm2 only)
- Port 3022. Taken ports: 3000, 3001, 3003, 3010, 3011, 3012, 3020, 3021, 4000. Never use them.
- Start: `pm2 serve . 3022 --name les-games && pm2 save`
- Restart: `pm2 restart les-games` | Stop: `pm2 stop les-games`
- Mac: http://localhost:3022 | Phone on same wifi: http://<Mac IP>:3022

## The games list (the only thing Matt edits to add a game)
- A `GAMES` array at the very top of the script, with a plain-language comment above it explaining how to add a game.
- Each entry: id, name, url, color (hex), icon (key of an SVG in the ICONS object), status ("live" or "soon").
- Current games: Wolf Sudoku (blue #5b8def, grid icon), Saloon Defense (orange #f28c38, saloon icon), High Noon (red #e63946, star icon), Ballin (gold #d4a017, basketball icon), Wurdle (green #3fa66b, wurdle icon).
- Real URLs come from Matt. Until he gives one, that game stays "soon".

## Locked decisions
- Tiles: 3 per row on phones, 5 per row on laptop (max page width 720px, centered).
- Each tile: rounded icon square, game name, and "Last played" text ("Just now", "2h ago", "3d ago", or "New").
- The whole tile is the link. Games open in the same tab so the phone's back button returns here.
- Order: live games first, most recently played first; never-played live games after played ones, in list order; then "soon" tiles.
- "Soon" tiles: faded, small "Soon" tag, not clickable.
- Last-played times saved in localStorage under `les-games:lastPlayed`, wrapped in try/catch. If storage fails, the page still works.
- Under the grid: one dashed "More games on the way" strip.

## Design (clean cartoony, NOT Wolf Creative)
- Page background cream #fff8ec. Outlines and text ink #1f1a2e. Muted text #8a8196.
- Tiles: white, 3px ink border, thicker 6px bottom border, 18px corners. Press effect: shifts down 2px.
- Header: small controller icon (red #ff6b6b) + "Les Games" in Fredoka 500, subtitle "Pick a game and go."
- Tap targets at least 44px. Sentence case. No emoji. No em dashes in any text.
- Visible keyboard focus ring on tiles for laptop use.

## Rules for Claude Code
- Read this file at the start of every session.
- Keep everything in index.html except the manifest and icons.
- Before committing, open the page and confirm there are no console errors.
- Commit at the end of each phase: `Phase N: description`. Tick the checklist below.
- Do not add frameworks, build tools or packages.
- After completing each task, tell me clearly: what you did, what you created or changed, and what the next step is. If you run into a decision that requires my input, give me two options with your recommendation.

## Build status
- [x] Phase 1: Page and games list
- [x] Phase 2: Deploy to Vercel and add real links
- [x] Phase 3: Polish and home screen icon

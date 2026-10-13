# Baltimore Reference: project notes for Claude Code

## What this is
A Baseball-Reference-style static site for an MLB The Show Orioles dynasty (tracked from 2031). It's a single file, `index.html`: plain HTML, CSS and vanilla JS, with no build step and no dependencies. It's hosted on GitHub Pages and shared with friends.

## Data source
- Data lives in the Google Sheet **MLB The Show Dynasty Database**, ID `18-JSasCsqC_HYN0o8BgV3V9ydn5duE7AkDozFSmIxXo`.
- The page reads it live through Google's public `gviz` CSV endpoint (see `fetchPublic` in `index.html`). The sheet must be shared as **Anyone with the link: Viewer**.
- Inside claude.ai, the page uses the Google Sheets connector instead, via `window.claude.use("mcp")` and `get_values`. On GitHub Pages `window.claude` doesn't exist, so the public path is used. Keep both paths working.
- Tabs read: Seasons, Roster, Players, Award Finalists, Award Votes, Playoffs, 99 Club. Columns are matched by header name (`norm()` lowercases and underscores them), never by position.
- Never hardcode or embed sheet data in the page. Everything is computed at load time.

## Code map (inside the single `<script>` in index.html)
- **Loading:** `parseCSV`, `fetchPublic`, `fetchRange`, `loadAll`.
- **Model:** `build(raw)` turns sheet rows into `DB`: seasons, roster, players, finalists, votes, playoffs, club, team totals `T`, and per-player aggregates. These include OPS+/ERA+ (relative to that season's Orioles lineup and staff), legacy score, similarity, rings and alumni.
- **Components:** sortable `table()`, SVG charts `lineChart`, `barChart` and `scatter`, plus `fig()`.
- **Views** (hash routes): `vHome`, `vSeasons`, `vSeason`, `vPlayers`, `vPlayer`, `vCompare`, `vLeaders`, `vAnalytics`, `vProjections`, `vTimeline`, `vLeague`, `vTeam`, `vHof`, `vTrivia`, `vGlossary`.
- **Trivia:** `GENS` holds question generators drawn only from dynasty data. The daily challenge is seeded by date and data size (`dailySeed`), so everyone gets the same questions. Progress and streaks are saved in `localStorage`.
- **Player card PNG:** `drawCard` (canvas) and `openCard` (dialog plus download).

## Conventions
- **Design:** cream/navy with Orioles orange. Fonts are Oswald (display) and IBM Plex Sans Condensed (body). Colors are CSS variables on `:root` with a dark theme. Keep it responsive and accessible: visible focus, keyboard-sortable tables, reduced motion.
- **Missing data:** blank means unknown; never invent values. Career rate stats are averages of season figures, because at-bats and innings aren't tracked.
- **Link previews:** `og:image` and `twitter:image` should be the absolute GitHub Pages URL of `og-image.png`.

## Testing
No test suite is checked in. To test locally, serve the folder with `python3 -m http.server` and open `http://localhost:8000`. The sheet must be publicly viewable for live data.

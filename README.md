# Boys Golf Trip 2027

Team Blue vs Team Green. June 15 to 18, 2027, Sandhills, NC.

A single-file site: countdown, tee sheet, live cup tug-of-war, pairings reveal, MVP race, add-to-calendar, prize pool and rosters.

## Hosting
Served as a static site with GitHub Pages. In the repo, go to Settings, then Pages, choose "Deploy from a branch", pick `main` and `/ (root)`, and save.

## Editing
All players, teams, matchups, scores and winners live in the single `trip-data` JSON block in `index.html`; everything else is derived from it. Add `?demo` to the URL to preview with fake data. See `CLAUDE.md` for the structure and the current open items.

Live URL: https://youngdesi2.github.io/golf-trip/

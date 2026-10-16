# Boys Golf Trip 2027 site

Single-file static website (`index.html`, no build step) for a 20-man Ryder Cup golf trip: Team Blue vs Team Green, June 15 to 18, 2027, in the North Carolina Sandhills. It is shared by URL with the group and meant to be hosted on GitHub Pages. The owner wants it to look pretty impressive.

## Trip facts
- Dates: Tue June 15 to Fri June 18, 2027. Lodging: Talamore Golf Villas.
- 20 players, 10 per team. Captains: Team Blue, Jeffrey "G" Giovannone. Team Green, Justin Palermo. 14 of 20 players are confirmed (listed in `CONFIG.pool`, captains included); 6 spots are still open and nobody has been assigned to a team yet.
- Rounds (first tee, local time): 
  - Tue 6/15: Talamore Golf Club 8:00 AM, Mid South Club 2:00 PM
  - Wed 6/16: Mid Pines 8:00 AM, Pine Needles 2:00 PM
  - Thu 6/17: Tobacco Road 8:00 AM, Southern Pines Golf Club 2:00 PM
  - Fri 6/18: Tot Hill Farm 9:00 to 9:40 AM
- Round formats are TBD. Matchups are TBD (5 placeholder matches per round for now).
- Prize pool: team match pot $5,000 (each man on the winning team collects $500), skins $600 a day, closest to the pin $400 a day. Trip MVP award, winner TBD.

## How the page is built
- Principle: enter data once. Everything that can change lives in ONE JSON block, `<script type="application/json" id="trip-data">`, with a comment above it explaining each field: `players` (name, team, captain, nick), `days` (skins and ctp winner names, plus `rounds` with course, url, start time, format, state, `revealed`, and `matches`), `mvp` (winner and point values), `updated`. Players are referenced by name everywhere, so spell names the same each time (the Live page warns about unknown names).
- Everything else is derived from that block: rosters and open spots, matchups, cup points and the tug-of-war bar, MVP leaderboard, skins/CTP per day, the pairings reveal, and the `.ics` calendar file. Fixed facts (dates, prize amounts, share URL, calendar event length) stay in `CONFIG` and `PRIZES` in the script below it.
- Trip page order: hero, Cup (tug-of-war), Tee Sheet, The Trip, Prize Pool, MVP. Each match shows two players per side (blank slots read TBD). Matchups on the tee sheet and the cards on the Teams page are collapsible (`.coll` pattern: button + animated grid-rows height, staggered fade-in of rows, open state remembered in `openKeys` so polling re-renders do not collapse them).
- Profiles and lore: optional `bio` and `tags` per player in `trip-data`. Only players with a bio or tags get a tappable name (small orange dot) that opens a bottom-sheet profile with their derived MVP stats. Optional `lore` array (`{title, text}`) renders "The Lore" section on the Trip page and stays hidden while empty. Demo mode includes fake examples. Never invent bios or jokes; use only what the owner or the group supplies.
- Views by URL hash, switched from a bottom dock: `#trip`, `#live`, `#pairings`, `#mvp`, `#rosters`.
- Cup bar: blue vs green tug-of-war, knot position = point difference over points needed to clinch (more than half of all matches). A dashed ghost knot shows "if it ended now" from live `lead` values. Confetti when a team clinches (once per session).
- Pairings reveal: `round.revealed` = how many matches are public (0 hides all, null shows all). Bump the number during the reveal; open pages animate the newly revealed cards and show a toast. "Replay the reveal" re-runs it for anyone.
- MVP race: points per player = match wins, halves, skins, closest to the pin, using the values in `mvp.points`. These defaults (win 1, halve 0.5, skin 1, ctp 1) are a placeholder the owner has not confirmed; the MVP prize and criteria are still TBD.
- Calendar: "Add to calendar" builds an `.ics` in the browser (7 events, one per round, with a stable UID so re-importing updates them). Start times are Eastern (EDT, UTC-4); each event is `CONFIG.calHours` long (5) because the schedule only has tee times.
- Live refresh: every open page re-reads `trip-data` from its own URL every 45 seconds and when the tab regains focus. Editing the block on GitHub and committing updates everyone after Pages redeploys (about a minute).
- Demo: add `?demo` to the URL (`https://youngdesi2.github.io/golf-trip/?demo`) to preview every feature with fake players and scores. Demo data is generated in `makeDemo()` and never touches the real data.
- Motion: hero contour lines and waving pin, staggered hero entrance, scroll reveals, ticking countdown digits, count-up scores, sliding dock indicator, view transitions. All respect reduced motion.
- Share preview: `og.png` (1200x630) plus Open Graph and Twitter tags pointing at `https://youngdesi2.github.io/golf-trip/`. If the repo or Pages URL changes, update the absolute URLs in the head and `CONFIG.shareUrl`.
- Fonts: Big Shoulders Display, Instrument Sans, DM Mono from Google Fonts. Single committed dark green look.

## Decisions and constraints
- Do not show what each person pays in. Show only the pools and who can win them.
- The bet breakdown the owner gave does not yet add up to the total he stated. Ask before showing any grand total.
- The owner disliked small illustrated course thumbnails. Do not add them back. Real photos are fine if he supplies them.
- Course names link to each course's official site (opens in a new tab).
- Keep it one HTML file with no build step unless the owner asks otherwise. `og.png` is the only other asset, needed because link previews require an image file.
- Phone first. Most of the group will open the link from a text message.

## Open items
- Names for the last 6 players, and team assignments for all 18 non-captains
- Formats and matchups for each round
- The remaining part of the bet total
- MVP criteria or prize
- Confirm the MVP point values (currently a placeholder)
- Optional extras: real course photos (only if supplied), per-hole scoring

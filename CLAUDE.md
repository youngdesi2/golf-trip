# Boys Golf Trip 2027 site

Single-file static website (`index.html`, no build step) for a 20-man Ryder Cup golf trip: Team Blue vs Team Green, June 15 to 18, 2027, in the North Carolina Sandhills. It is shared by URL with the group and meant to be hosted on GitHub Pages. The owner wants it to look pretty impressive.

## Trip facts
- Dates: Tue June 15 to Fri June 18, 2027. Lodging: Talamore Golf Villas.
- 20 players, 10 per team. Captains: Team Blue, Jeffrey "G" Giovannone. Team Green, Justin Palermo. The other 18 players are TBD.
- Rounds (first tee, local time): 
  - Tue 6/15: Talamore Golf Club 8:00 AM, Mid South Club 2:00 PM
  - Wed 6/16: Mid Pines 8:00 AM, Pine Needles 2:00 PM
  - Thu 6/17: Tobacco Road 8:00 AM, Southern Pines Golf Club 2:00 PM
  - Fri 6/18: Tot Hill Farm 9:00 to 9:40 AM
- Round formats are TBD. Matchups are TBD (5 placeholder matches per round for now).
- Prize pool: team match pot $5,000 (each man on the winning team collects $500), skins $600 a day, closest to the pin $400 a day. Trip MVP award, winner TBD.

## How the page is built
- All content is data in the script at the bottom of `index.html`: `CONFIG` (dates, teams, captains), `DAYS` (rounds, tee times, matches, skins and ctp winners), `PRIZES`, `MVP`, `COURSE_URLS`. Update those and the page re-renders. Cup points are computed from match `winner` values (`'blue'`, `'green'`, `'halved'`).
- Two views, Trip and Rosters, switched by `#trip` and `#rosters` in the URL hash.
- The hero has a canvas of drifting topographic contour lines with a pin flag. It respects reduced motion.
- Fonts: Big Shoulders Display, Instrument Sans, DM Mono from Google Fonts. Single committed dark green look.

## Decisions and constraints
- Do not show what each person pays in. Show only the pools and who can win them.
- The bet breakdown the owner gave does not yet add up to the total he stated. Ask before showing any grand total.
- The owner disliked small illustrated course thumbnails. Do not add them back. Real photos are fine if he supplies them.
- Course names link to each course's official site (opens in a new tab).
- Keep it one file with no build step unless the owner asks otherwise.
- Phone first. Most of the group will open the link from a text message.

## Open items
- Names and team assignments for the other 18 players
- Formats and matchups for each round
- The remaining part of the bet total
- MVP criteria or prize
- Ideas to make it more impressive, for example a share preview image, scoring during the trip, per-round results

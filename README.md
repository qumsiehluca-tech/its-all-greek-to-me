# It's all Greek to me

A daily word game played with Greek letters that look like English ones: Η is H, ρ is p, ς is s. Build as many words as you can from the day's bin of tiles and climb the Greek alphabet from Omega to Alpha.

**[Play it](https://qumsiehluca-tech.github.io/its-all-greek-to-me/)**

## Modes

| Mode | Tiles | Notes |
| --- | --- | --- |
| Easy | 12 capitals | Capital Greek letters only |
| Medium | 10 lowercase | Final sigma (ς) can only end a word |
| Hard | 8 lowercase | Tile labels hidden |
| Keystone | 6 lowercase | A centre tile must appear in every word; using all six earns +10 |

## How it's built

- One static `index.html`: vanilla JS, no framework, no build step, no backend.
- **Deterministic daily puzzle.** The date seeds a PRNG (mulberry32 over an FNV-1a hash), so every player gets the same bin each day with no server.
- **Fairness guarantees at generation time.** Each mode enumerates every possible tile combination and only keeps bins that can spell a minimum share of common words (30% for Easy/Medium, 15% for Hard). Keystone requires at least 25 words through the centre tile and at least one common word that uses every tile. Bins are bit-masked (one bit per letter) so these checks run in the browser at load.
- **Scoring.** Letters are weighted by rarity, repeats in a word score half, and the rank (Omega → Alpha) is derived from total points against the best achievable in that bin.
- Progress is stored in `localStorage`; the share card is plain text with no tracking.
- Accessible: keyboard play, ARIA labels on tiles, light/dark themes, reduced-motion support.

## Run locally

Open `index.html` in a browser.

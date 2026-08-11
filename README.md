# OSRS Skilling Supply Planner

A single-file web tool that works out **how many of each supply** you need to take
an Old School RuneScape account to **99 in every non-combat skill** — chained from
your *current* XP, not just the final method.

Unlike a single-method cost calculator, it counts the whole journey: pick a training
method per skill and it sums the supplies and GP from where you are now to level 99,
including the level breakpoints where methods change over.

Built for the account **24 Weetbix** (main, defence build → 99 all non-combat), but it
works for any account — just load its stats.

## Use it

Open `index.html`. No build step, no dependencies, nothing to install.

**Update your stats — three ways:**

1. **Paste JSON** (works everywhere, including inside the Claude app).
   Open one of these and paste the whole response into the box, then *Update from JSON*:
   - TempleOSRS: `https://templeosrs.com/api/player_stats.php?player=<RSN>&bosses=1`
   - Wise Old Man: `https://api.wiseoldman.net/v2/players/<RSN>`
2. **Edit a level inline** — change any skill's current level for quick "what if I do X first" checks.
3. **Fetch live (Wise Old Man)** — enter an RSN and pull straight from the WOM API.
   The button asks WOM to refresh the account from the official hiscores, then loads it.
   Requires the account to be tracked on WOM. Works on GitHub Pages / when opened locally;
   **blocked inside the Claude app sandbox** — use paste there.

**Then:** choose a method per skill from the dropdown and edit any XP rate or GE price.
The consolidated shopping list and totals recompute live.

## Host on GitHub Pages

1. Put `index.html` in the repo root.
2. **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `/ (root)`**.
3. It goes live at `https://<user>.github.io/<repo>/`.

The live WOM fetch works on Pages because it's served from a real HTTPS origin and the
WOM API is CORS-friendly.

## Notes & accuracy

- **Prices are placeholders.** Set them to live GE prices before trusting the gp total.
- **XP/action rates** are one sensible method each and are fully editable — swap freely.
- **Level gaps:** if a method unlocks above your current level, those lower levels show as
  "not costed" — pick a lower-tier method in the dropdown to include them.
- **Sells back:** Smithing bars and Herblore potions recover most of their raw cost on
  resale, so the gross gp figure overstates real spend.
- **Firemaking** defaults to Wintertodt (free, no supplies). **Slayer** needs combat and is
  excluded on a 1-attack build. **Farming** is run-based (tree/herb runs), not a bulk order.
- **TempleOSRS direct fetch** isn't possible from a static page (no CORS headers). Use paste,
  the WOM live button, or put a small proxy / Cloudflare Worker in front of the Temple API
  if you specifically want Temple.

The XP curve uses the exact OSRS experience formula, so every level → XP figure is precise.

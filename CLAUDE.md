# Repository guide for Claude Code

Single-file web app: `index.html` is an OSRS skilling supply planner (works out how
many of each supply an account needs to reach 99 in every non-combat skill, chained
from current XP). No build step, no dependencies — open `index.html` directly.
`README.md` documents usage.

## Standing workflow instructions

The owner wants changes shipped to GitHub end-to-end without being asked each time:

- **Always push to GitHub.** After a change, commit and push to the working branch —
  never leave changes only on local disk.
- **Always open a pull request** for every change, automatically (no need to ask).
- **Auto-merge the PR** into `main` once it's open. This repo has no CI checks, so PRs
  are mergeable immediately; use the squash merge method.
- **After a PR is merged, start fresh:** a merged PR is finished and must not be reused.
  Restart the working branch from the latest `main`
  (`git fetch origin && git checkout -B <branch> origin/main`) and open a new PR for the
  next change. Never stack new commits on already-merged history.

## Implementation notes

- Prices in the planner are editable placeholders. The **Fetch live GE prices** button
  pulls real values from the OSRS Wiki prices API (`prices.runescape.wiki`) via the
  `ITEM_IDS` name→id map. Live fetches work when the page is hosted (e.g. GitHub Pages)
  but are blocked inside the Claude app sandbox — same as the Wise Old Man fetch.
- Training methods live in the `SKILLS` array; each method lists per-action item costs
  and xp rates, both editable in the UI. Keep xp/level/material values aligned with
  current OSRS / TempleOSRS figures.
- After editing the inline `<script>`, sanity-check that it still parses before pushing.

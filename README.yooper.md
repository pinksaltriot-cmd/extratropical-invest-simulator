> Yooper copy of `README.md` — da English original's right next to dis one, eh.

# Extratropical Invest Simulator

A standalone, deterministic simulator for da whole life of an extratropical (cold-core)
invest — da kind o' storm a fella up by Marquette knows real good. Punch in da environment — surface temperature, sea/land, shear, baroclinicity,
humidity, latitude, steering, invest strength, and advisory time — and ya get dat system's
evolution at 6-hour intervals: chance of formation, core pressure, track, size, winds,
core temperature, and precipitation (type + rate + accumulation) broken out by storm
region, plotted on a world track map.

Open `index.html` in any browser — no build step, no dependencies.
Run `index.html?selftest=1` to kick off da built-in engine test suite. It prints
`SELFTEST <pass>/<total> PASS|FAIL` to da console and to `#selftest .sum` in da page.

## Local dev notes, eh

**Dere's two `launch.json` files, and only one of 'em is live.** `preview_start` finds
`.claude/launch.json` from da *workspace root*, so inside da `Peter/` workspace da
live config is `Peter/.claude/launch.json` (its `eis` entry serves dis repo via
`--directory extratropical-invest-simulator`). Da copy at `.claude/launch.json` in dis
repo only counts for a standalone clone, where da server runs from da repo root and
don't need no `--directory` flag. Dis repo can't version da workspace-root file. If ya
edit da repo-local copy inside da workspace and nuttin' changes, dat's why — go edit da
workspace-root one instead.

**Reloads get cached, cripes.** `python -m http.server` plus browser caching will happily hand ya
da *previous* `index.html` after ya edit it, so da selftest can report a stale PASS
against pre-edit code. Always tack on a fresh cache-buster — `?selftest=1&cb=<something-new>` —
and read da result from `#selftest .sum` in da live DOM, not from da console
history, 'cause dat hangs onto lines from earlier runs like a pasty in yer pocket.

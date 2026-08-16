# Extratropical Invest Simulator

A standalone, deterministic simulator for the life cycle of an extratropical (cold-core)
invest. Enter the environment — surface temperature, sea/land, shear, baroclinicity,
humidity, latitude, steering, invest strength, and advisory time — and get the system's
evolution at 6-hour intervals: chance of formation, core pressure, track, size, winds,
core temperature, and precipitation (type + rate + accumulation) broken out by storm
region, plotted on a world track map.

Open `index.html` in any browser — no build step, no dependencies.
Run `index.html?selftest=1` to execute the built-in engine test suite. It prints
`SELFTEST <pass>/<total> PASS|FAIL` to the console and to `#selftest .sum` in the page.

## Local dev notes

**Two `launch.json` files exist, and only one is live.** `preview_start` resolves
`.claude/launch.json` from the *workspace root*, so inside the `Peter/` workspace the
live config is `Peter/.claude/launch.json` (its `eis` entry serves this repo via
`--directory extratropical-invest-simulator`). The copy at `.claude/launch.json` in this
repo applies only to a standalone clone, where the server runs from the repo root and
needs no `--directory` flag. This repo cannot version the workspace-root file. If you
edit the repo-local copy inside the workspace and see no effect, that is why — edit the
workspace-root one.

**Reloads are cached.** `python -m http.server` plus browser caching will happily serve
the *previous* `index.html` after you edit it, so the selftest can report a stale PASS
against pre-edit code. Always append a fresh cache-buster — `?selftest=1&cb=<something-new>` —
and read the result from `#selftest .sum` in the live DOM rather than from console
history, which retains lines from earlier runs.

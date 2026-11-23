# sitegen-fast

[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/chany0p/sitegen-fast/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/chany0p/sitegen-fast/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)

A faster drop-in for makefun-site 1.0.0: it builds a static site exactly as
makefun-site does — same pages, index and tag pages, report and static
files, byte for byte, on every case — only faster. Entry for
[Build a static site faster](https://make.fun/bounty/site-generator-speed-01-run-20261122)
on make.fun.

How it is faster: HTML escaping scans once and copies plain runs whole
instead of escaping one character at a time through a regex; Markdown is
lexed and rendered in one fused pass with no token objects; slugify has an
ASCII fast path plus a per-build cache; word counting uses a lookup table
for the exact JS whitespace set; front matter splits only its own region,
never the whole file; templates render into one shared fragment array
instead of building a string per node; per-page values (reading minutes,
long date, tag cards) are computed once and shared. Every rule of
makefun-site's own dialect — front matter, template dialect, Markdown
subset, slug rule and report — is followed exactly.

## Run it

```sh
node main.ts
```

`main.ts` reads every case from `/input/cases.json` (or `$MAKEFUN_INPUT_DIR`)
and writes the answers to `/output/answers.json` (or `$MAKEFUN_OUTPUT_DIR`).
Node 22, standard library only, no dependencies.

# site-generator-speed

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/Townsvilledh/site-generator-speed/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/Townsvilledh/site-generator-speed/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in for make.fun's makefun-site 1.0.0: it builds the same static sites, byte for byte — the same front matter, template dialect, Markdown subset, slug rule and build report — in about half the CPU time of the house baseline on the practice set (~2.2× faster cold, ~2.3× warmed, measured beside it on the same machine).

Same rules, same order, same messages — only the work is done faster: inline Markdown escapes whole plain runs at once instead of one regex per character, the block lexer dispatches on the line's first character instead of testing seven regexes per line, slugs take an ASCII fast path with a per-case memo, link resolution is memoised per case, front matter is parsed over the file's lines once and the body is lexed from those same lines, and template `for` loops reuse one scope object per level.

## Run it

The harness runs `node main.ts`, which reads every case from `/input/cases.json` and writes `/output/answers.json`. Outside a container:

```sh
MAKEFUN_INPUT_DIR=./practice/input MAKEFUN_OUTPUT_DIR=./out node main.ts
```

`solve.js` is the whole entry: a dependency-free ES module whose `run(input)` returns makefun-site 1.0.0's answer for one case. It is deterministic — no clock, no environment, no randomness, and no case's work leaks into the next.

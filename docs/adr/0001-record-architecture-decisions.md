---
status: accepted
date: 2026-11-22
---

# Record architecture decisions

We record decisions that are costly to reverse or surprising to a newcomer as short Markdown files in `docs/adr/`, numbered sequentially (`0002-...`), each with a status and date in front matter. Agents and humans read the relevant ADRs before working in the area they touch.

Why: the repo vendors a large upstream tree and layers an SDK over it, so the reasons for local choices are otherwise lost in commit history.

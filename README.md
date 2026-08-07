# PPR — Prompt, Pray, Repeat

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code Plugin](https://img.shields.io/badge/Claude%20Code-Plugin-5A32A3)](https://docs.claude.com)
[![Status](https://img.shields.io/badge/status-early%20development-orange)]()

A suite of Claude Code tools for teams doing serious agentic development —
built around a simple idea: **persistence without reflection is just stubbornness.**

This isn't one tool. It's four independent tools that share a data layer and
ship together as one plugin:

| Tool | Command | What it does |
|---|---|---|
| **Council** | `/council` | Convene a defined panel of personas to reason through a question, cross-examine each other, and synthesize a recommendation. |
| **Examen** | `/examen` | A daily/weekly report on what your agents did, what they got wrong, and concrete corrections — with a team retro mode. |
| **Retreat** | `/retreat` | Step a project or question away from active work for several rounds of contemplative iteration, returning one small, high-value insight. |
| **PPR (loop)** | `/ppr` | The original persistent-execution loop concept — evidence-driven iteration with strategy-stagnation detection and escalation. Deprioritized until the other three exist and produce real data. |

## Install

```
/plugin marketplace add PromptPrayRepeat/PPR
/plugin install ppr@PromptPrayRepeat
```

(Adjust once the marketplace listing is live — see `plugin.json` for the
current command manifest. Council, Examen, and Retreat are the commands
available today; `/ppr` is not yet built, see `docs/ppr-loop.md`.)

## Design principles

1. **Independent-first, coupled-by-schema.** Every tool must be useful on its
   own, with zero dependency on the others being installed or invoked. They
   compose through a shared on-disk data format (see
   [`docs/shared-schema.md`](docs/shared-schema.md)), not through shared code
   paths or runtime coupling.

2. **Skills over infrastructure.** Nothing in this suite needs a server, a
   database, or its own UI in v1. Claude Code's native primitives — skills,
   subagents, hooks, and file I/O — are sufficient for everything specified
   here. Reach for more only when usage data says so.

3. **One plugin, four commands.** Single repo, single marketplace listing,
   single install. Someone installs this for one reason and discovers the
   rest by using it.

4. **The devotional framing is a feature, not a bit.** Confession-shaped
   self-review gets read where dry logs get skipped. Keep the tone
   throughout, but never let a name outrun its function — see the naming
   notes in each tool's doc.

5. **Team-scale, not solo-dev-scale.** Every tool should have a sane answer
   to "what does this look like when five people on a team are using it,"
   even if that answer is "not built yet, but not precluded."

## Build order

Built in this order so each tool is independently shippable and the later
ones inherit a working schema instead of guessing at one:

1. **Examen** — smallest scope, no dependencies, immediate personal value.
   Also the forcing function for getting the shared schema right early.
2. **Council** — standalone value; also becomes PPR's Independent Review
   mechanism for free once it exists.
3. **Retreat** — benefits from Council's multi-round convergence pattern
   already existing.
4. **PPR loop** — by this point, decide whether the original stagnation-
   detection mechanic is still worth building, or whether `/goal` (Claude
   Code's native completion-loop primitive) plus the three tools above
   already covers the need. Don't build this speculatively — build it once
   Examen data says it's needed.

## Repo structure

```
PPR/
├── README.md
├── plugin.json                  # plugin manifest (name, commands, version)
├── docs/
│   ├── shared-schema.md         # the .ppr/ data layer every tool reads/writes
│   ├── council.md               # /council spec
│   ├── examen.md                # /examen spec
│   ├── retreat.md               # /retreat spec
│   └── ppr-loop.md              # /ppr spec (future work, stub for now)
├── skills/
│   ├── council/SKILL.md
│   ├── examen/SKILL.md
│   ├── retreat/SKILL.md
│   └── ppr/SKILL.md             # not built yet
└── stakeholders/                # example personal stakeholder library
    └── example-panelist.json
```

## Naming notes

- The suite name and account are **Prompt, Pray, Repeat**.
- The original PRAY acronym (Pause / Review / Assess / Yield) from the first
  design pass is **not committed to** — the loop tool may end up structured
  differently once Council, Examen, and Retreat exist. Don't build tooling
  that assumes the acronym is load-bearing.
- **Retreat** is the working name for the contemplative-iteration tool
  (previously drafted as "Deep Prayer," rejected for colliding with PRAY;
  "Meditate" and "Discernment" were runners-up — revisit only if Retreat
  stops fitting once built).

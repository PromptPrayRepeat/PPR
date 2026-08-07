# Contributing

PPR is early — the four tools in `docs/` range from "spec, not yet built"
to "not yet designed." That's worth knowing before opening a PR.

## Where things stand

Check `README.md`'s build order before assuming a tool exists. As of this
writing, expect specs before implementations — issues and design feedback
are more useful than code right now for anything not yet marked built.

## Good ways to contribute at this stage

- **Try the spec, not just the code.** If you write a stakeholder JSON file
  per `docs/council.md` and it doesn't behave the way the doc implies once
  Council exists, that's a more valuable report than a style nit.
- **Naming and framing feedback.** The devotional naming (Council, Examen,
  Retreat) is a deliberate choice, not locked in stone — see the naming
  notes in `README.md` and `docs/retreat.md` if you think something's not
  landing.
- **Schema feedback on `docs/shared-schema.md`** before it's frozen with a
  `schema_version` — this is the one thing genuinely expensive to change
  once tools depend on it.

## Once there's code

Standard fork/branch/PR flow. Keep each tool's skill self-contained per the
"independent-first, coupled-by-schema" principle in the README — a PR that
adds a dependency from one tool's skill directly into another's internals
(rather than through `.ppr/log.jsonl`) is going against the project's core
design constraint and will get pushback regardless of how clean the code is.

## Issues

Use issues for design disagreements, not just bugs — at this stage, "I
don't think Retreat's output constraint should be this strict" is exactly
as welcome as a bug report.

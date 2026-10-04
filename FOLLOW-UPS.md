# Follow-ups for this fork

<!-- SITE-05@v1: The CLI risk below changes how enforcement reaches the tools, so it is recorded beside the system it serves. -->

This branch carries Bear's version of the method. Upstream is
`Principle-Driven/pdd`. This file records the open work and the decisions
that keep the fork coherent.

## CLI risk: the pdd command follows the working tree

`~/.local/bin/pdd` is a symlink to `packages/cli/src/cli.mjs` in the clone
of this fork. The command runs whatever branch that clone has checked out.
A checkout of `main` silently reverts every tool to upstream behavior,
including the accepted-risk fix. Before you rely on `pdd` after any branch
switch in this repository, confirm the branch is `bear/version`.

A durable alternative is a published package from this fork, installed as
a pinned development dependency in each tool. No tool currently needs that
strictness.

## Offer the accepted-risk fix upstream

The scanner read `pdd.config.json` as a citation site, so the bare
`acceptedRiskPrinciple` token always failed the check. Any adopter of the
accepted-risk catalog entry received a permanently red build. This fork
fixes it: the config file stays out of citation scanning, the setting
accepts a bare or a pinned token, and a stale pin reports PDD203.

Offered upstream as [Principle-Driven/pdd#1](https://github.com/Principle-Driven/pdd/pull/1)
from the `fix/accepted-risk-enforcement` branch. Until it merges, this
fork carries the fix.

## Shared principle family policy

The CLI validates one token prefix against one principle directory per
repository. Cross-repository token citations cannot resolve, so the shared
family works this way:

- The canon lives in this fork's catalog. PDD-07 states the preview and
  apply command grammar. PDD-08 keeps rule titles prose-rare.
- Each tool adapts the canon rule under its own prefix and version, with
  an honest history entry.
- A lineage section may name the catalog entry in prose. It must not cite
  a catalog token, because the tool's scanner cannot resolve it.
- The source of the shared grammar is the `bin-creator` skill and the
  Ruby program design guide: plan before apply, fixed exit codes, split
  streams, and network-free suites.

## Tool adoption status

| Tool | Prefix | State |
| -- | -- | -- |
| github-stars | GHS | Adopted. Four rules, `rake quality` runs the check. |
| spokenly | SPK | Adopted. Four rules, `rake quality` runs the check. |
| hn-summary | HN | Adopted. Three rules, `rake quality` runs the check. |
| secret | SEC | Adopted. Three rules, new agent index, offline suite gate. |

The recipe for the next tool: read its agent guidance and tests, extract
only the judgments that earned their rule, cite tokens at the code sites
that depend on them, and wire the check into the tool's quality task.

## Decision: no baseline mode

A tolerance baseline would freeze today's findings as accepted exceptions.
That contradicts the reconstruction idea at the heart of the method: the
check must read current evidence, not a remembered list of failures. The
`ignore` setting in each tool config is the sanctioned escape during a
retrofit, and it must shrink, not grow.

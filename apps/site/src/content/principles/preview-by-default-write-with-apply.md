---
token: PDD-07@v1
title: Preview by default, write only with apply
summary: A command that changes state previews its changes by default and writes only when the user passes an explicit apply flag.
benefit: One flag boundary replaces a careful reading of each command help text before every run.
prevents: Agents do not run write-mode commands before a person reviews the planned changes.
category: Reliability
version: v1
published: 2026-10-04
updated: 2026-10-04
order: 7
useWhen: A command creates, changes, or deletes files, remote state, or published output.
tradeoff: Each command must keep two correct paths, the preview and the apply.
lineage: Plan and apply workflow (Terraform); dry-run flags in package managers.
---

## Rule

A command that changes state previews its changes and writes nothing by default. The command writes only when the user passes an explicit apply flag.

Keep the exit codes fixed. Use 0 for success or a clean tree, 1 for findings or errors, and 2 for a usage error. Send narration to stderr. Send operation detail and machine output to stdout.

## Benefit

An agent or a person can run the bare command, read the plan, and then apply it. Scripts can trust the exit codes and the stream split. No run destroys state by accident.

## Problem this prevents

Agents run write-mode commands before anyone reviews the plan. A wrong flag then deletes or rewrites derived data that took a long job to produce. Mixed streams break scripts that parse stdout.

## What this changes

- Writers gate every write behind the apply flag.
- Writers keep the preview complete; the preview must show the exact plan.
- Reviewers reject a change that writes in preview mode or moves a stream.
- Readers can run the bare command on production data without risk.

## Exceptions

A command inside a transaction that can restore the previous state can write without a flag. Name the restore path when you omit the flag.

## Start here

List the commands that change state. Add the flag boundary to each. Then test that the bare run writes nothing.

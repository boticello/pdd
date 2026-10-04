---
token: PDD-08@v1
title: Choose prose-rare titles
summary: Give each principle a title that ordinary repository prose cannot use by accident.
benefit: The title-form check stays a useful signal, because each hit points to text that discusses the rule.
prevents: Adopters do not ignore or disable the title-form check after it flags coincidental phrases.
category: Governance
version: v1
published: 2026-10-04
updated: 2026-10-04
order: 8
useWhen: You name a principle in a repository that enforces pins on title-form references.
tradeoff: A title can sound less natural than the common phrase for the same idea.
---

## Rule

A principle title must not be a phrase that ordinary repository prose can use by accident. Before you adopt a title, search the repository for the full phrase. If the phrase appears in prose, make the title more specific.

## Benefit

The title-form check stays a useful signal. Each hit points to text that discusses the rule, so a nearby pin is the correct fix.

## Problem this prevents

A generic title appears in many sentences that cite no rule. The checker flags each one. The team then ignores the check or disables it, and real rule references pass unseen.

An adoption trial on a Ruby tool produced this failure. A readme sentence repeated a principle title word for word, and the checker demanded a pin for a sentence that cited no rule.

## What this changes

- Writers search the repository for a candidate title before they adopt it.
- Reviewers reject a title that already occurs in prose without a pin.
- Readers can treat each title-form hit as a probable rule reference.

## Exceptions

The principle file itself can repeat its title. The scanner does not read principle files as citation sites.

## Start here

Pick the clearest phrase for the rule. Search the repository for that exact phrase. If it occurs in prose, make the title more specific.

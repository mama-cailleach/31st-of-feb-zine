---
layout: page
title: Game Tables Spec
permalink: /tables-spec/
---

This page defines the structured data that the companion program will embed.

## Schema Summary

- `schema_version`: version pin for parser compatibility
- `core_rules`: fixed constants for DC, battery, stability, and loop behavior
- `narrative_resolution`: defines how pre-roll prompts and post-roll flavor are connected
- `pools`: stat labels and character creation constraints
- `sip_rules`: persistent SIP economy rules
- `os_table`: stability range lookup for The OS die behavior
- `random_flavor_tables`: optional prompt generators for Success flavor and Glitch events
- `seasons`: ordered season list with objective IDs
- `objective_catalog`: normalized objective definitions keyed by unique IDs

Unique objective IDs are season-scoped to avoid collisions.

- `AW_*` = Awakening
- `CM_*` = Journey
- `IN_*` = Interview
- `RT_*` = Return

Each objective includes:

- display `symbol` (D/O/W, G/L/Y, S/T/A/R, B/U/M)
- display `name`
- `season_id`
- suggested `default_pool`
- `pool_options`
- optional `prompt_die` + `prompts`
- optional `special_check` metadata (Interview Result, Return Recharge, Return Receipt Printing)

Prompt usage model:

- Objective `prompts` are scene setup text shown before the roll.
- After resolving the roll, flavor is selected by `narrative_resolution.outcome_flavor`.
- Success flavor uses `architecture_of_success` and is keyed by the pool used (`msk`, `sns`, `log`).
- Glitch flavor uses `big_book_of_glitches`.
- If total equals DC, apply the equal-DC glitch overlay rule and penalty.

Return station specifics:

- `RT_G` (Commute Back) is the only check that applies Exhaustion dice capping.
- `RT_H` (Recharge) is a d100 check with battery carryover rules.
- `RT_I` (Receipt Printing) records loop summary output, including Success and Glitch counts.

Random flavor specifics:

- `architecture_of_success` uses d12 and is split by pool (`msk`, `sns`, `log`).
- `big_book_of_glitches` uses d20 when total equals DC and applies a Stability penalty.

## Data Targets

- `seasons`
- `objective_catalog`
- `os_table`
- `random_flavor_tables`
- `narrative_resolution`
- `core_rules`
- `sip_rules`

See `_data/tables.json` for the machine-readable source of truth.

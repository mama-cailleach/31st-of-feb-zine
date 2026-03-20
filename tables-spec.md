---
layout: page
title: Game Tables Spec
permalink: /tables-spec/
---

This page defines the structured data that the companion program will embed.

## Schema Summary

- `schema_version`: version pin for parser compatibility
- `core_rules`: fixed constants for DC, battery, stability, and loop behavior
- `pools`: stat labels and character creation constraints
- `sip_rules`: persistent SIP economy rules
- `goddess_table`: stability range lookup for Goddess die behavior
- `seasons`: ordered season list with objective IDs
- `objective_catalog`: normalized objective definitions keyed by unique IDs

Unique objective IDs are season-scoped to avoid collisions.

- `AW_*` = Awakening
- `CM_*` = Commute
- `IN_*` = Interview
- `RT_*` = Return

Each objective includes:

- display `symbol` (A/B/C...)
- display `name`
- `season_id`
- suggested `default_pool`
- `pool_options`
- optional `prompt_die` + `prompts`
- optional `special_check` metadata (for Interview Result)

## Data Targets

- `seasons`
- `objective_catalog`
- `goddess_table`
- `core_rules`
- `sip_rules`

See `_data/tables.json` for the machine-readable source of truth.

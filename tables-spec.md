---
layout: page
title: Game Data Notes
permalink: /tables-spec/
---

This page documents the active JSON schema used by both the zine and the planned companion app.

## Schema Overview

- `schema_version`
- `game_metadata`
- `character`
- `rules`
- `random_events`
- `lore`

## Key Rule Payloads

- Loop cadence: one d100 event per phase, four phases per loop.
- Battery hindrance: hard stop when Battery reaches 0.
- Stability maintenance: Compliance restore (`Battery -5`, `Stability +5`) once per phase.
- Probability threshold: trigger when running product reaches `<= 0.1%`.
- Threshold effect: apply both `Stability -10` and `SIP +1`.

## Random Event Data

`random_events.events` contains 100 indexed entries.

Each event entry includes:

- `roll`
- `prompt`
- `category`
- `default_probability`
- `battery_delta`
- `stability_delta`
- `tags`

## Companion App Target

This schema supports:

- d100 event rolling
- stat updates per event
- running probability calculation
- threshold trigger detection
- loop receipt generation

Implementation-ready payload examples are in [Companion App Contract](/companion-app-contract/).

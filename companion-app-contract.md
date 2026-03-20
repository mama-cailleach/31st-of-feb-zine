---
layout: page
title: Companion App Contract
permalink: /companion-app-contract/
nav_exclude: true
---

This page defines practical payload shapes for a future companion app using `_data/tables.json`.

Try the interactive version: [Companion App Prototype](companion-app-prototype/).

## Core Source

- Canonical game data file: `_data/tables.json`
- Event count: `random_events.table_size`
- Event list: `random_events.events`
- Rule constants: `rules`

## Session State Shape

```json
{
  "session_id": "loop-2026-03-20-001",
  "game_id": "31st-of-february",
  "phase_index": 1,
  "phase_id": "awakening",
  "stats": {
    "battery": 100,
    "stability": 100,
    "sip": 0
  },
  "rolled_events": [],
  "running_success_probability": 1.0,
  "threshold_triggered": false,
  "loop_status": "active"
}
```

## Event Roll Result Shape

```json
{
  "roll": 41,
  "event": {
    "roll": 41,
    "prompt": "A street vendor calls you Candidate.",
    "category": "unusual_deviant",
    "default_probability": 0.25,
    "battery_delta": -7,
    "stability_delta": -6,
    "tags": ["unusual_deviant", "street", "loop"]
  },
  "phase_id": "journey"
}
```

## Event Application Shape

Apply event deltas to current stats and clamp to bounds in `character.vital_signs`.

```json
{
  "before": {
    "battery": 92,
    "stability": 90,
    "sip": 0,
    "running_success_probability": 0.1
  },
  "applied": {
    "battery_delta": -7,
    "stability_delta": -6,
    "probability_factor": 0.25
  },
  "after": {
    "battery": 85,
    "stability": 84,
    "sip": 0,
    "running_success_probability": 0.025
  }
}
```

## Compliance Action Shape

Compliance can be used once per phase.

```json
{
  "action": "compliance_restore",
  "phase_id": "interview",
  "rule": {
    "battery_delta": -5,
    "stability_delta": 5,
    "usage": "once_per_phase"
  },
  "result": {
    "battery": 75,
    "stability": 86
  }
}
```

## Threshold Evaluation Shape

Threshold logic from data file:

- `rules.probability.threshold_decimal`
- `rules.probability.threshold_effect`

```json
{
  "running_success_probability": 0.001,
  "threshold_decimal": 0.001,
  "condition_met": true,
  "effect_applied": {
    "stability_delta": -10,
    "sip_delta": 1
  },
  "updated_stats": {
    "stability": 70,
    "sip": 2
  }
}
```

## Hard Stop Evaluation Shape

Battery hard-stop rule from `rules.battery.hard_stop_at_zero`.

```json
{
  "battery": 0,
  "hard_stop_at_zero": true,
  "outcome": "phase_ended_immediately",
  "loop_status": "stopped_on_battery"
}
```

## Loop Receipt Shape

```json
{
  "session_id": "loop-2026-03-20-001",
  "ended_by": "return_phase_complete",
  "final_stats": {
    "battery": 67,
    "stability": 72,
    "sip": 1
  },
  "rolled_event_count": 4,
  "running_success_probability": 0.00125,
  "threshold_triggered": false,
  "next_loop_date": "31st of February"
}
```

## Minimal App Flow

1. Load `_data/tables.json`.
2. Initialize session state with start stats.
3. For each phase in `rules.loop.phases`: roll d100, fetch event by roll, apply deltas, update probability.
4. Allow optional compliance once in current phase.
5. Evaluate threshold after each event.
6. If Battery hits 0 and hard stop is enabled, end phase/loop.
7. Emit loop receipt.

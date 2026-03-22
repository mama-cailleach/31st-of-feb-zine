---
layout: page
title: Terminal
permalink: /terminal/
---

Terminal play guide.
Simple and fast.

Play it from: [https://mama666.itch.io/31st-of-february](https://mama666.itch.io/31st-of-february)

## What the Terminal Does

- Displays prompts and station flow
- Resolves commands
- Tracks resources
- Shows objective transitions
- Supports auto or manual dice mode

## Core Commands

### Session Commands

- start
- reset
- quit
- help
- status
- export

### Character Setup

- type your name as plain text during name prompt
- archetype camouflage
- archetype strategist
- archetype runner

### Rolling Commands

- roll msk
- roll sns
- roll log
- roll commute
- roll result
- roll recharge

### Utility Commands

- sip spend
- print receipt
- mode auto
- mode manual
- manual <dice values>
- sound on
- sound off
- music on
- music off
- sfx on
- sfx off

## Command Meanings (Quick)

- status: current loop/resources summary
- export: download transcript
- sip spend: negate next OS modifier
- print receipt: finalize loop receipt step
- mode manual: you enter dice values yourself
- sound on/off: global sound toggle (same as header sound button)
- music on/off: background loop only
- sfx on/off: terminal blips only

## Manual Dice Rules

Use manual only when manual mode is on.

- For pool and commute rolls: enter d6 values
- For result and recharge: enter one d100 value
- Enter values as space-separated numbers

Examples:

- manual 6 3 4
- manual 72

## Quick-Start Flow

1. start
2. enter name
3. archetype strategist (or any archetype)
4. roll your prompted objectives
5. at Result objective: roll result
6. at Commute Back: roll commute
7. at Recharge: roll recharge
8. at Receipt: print receipt
9. continue next loop or quit

## Reading Terminal Output

Look for these lines:

- Station: where you are
- Objective: what you are resolving now
- Prompt: scene setup text
- Total vs DC: success or glitch result
- Battery/Stability changes: current risk state

## Common Mistakes

- Rolling the wrong command for current objective
- Forgetting print receipt at Receipt objective
- Entering invalid manual dice values
- Spending SIP outside a valid roll phase

## Troubleshooting

If stuck:

- type help
- type status
- type reset

Audio control options:

- use the Sound button in the terminal header for quick global toggle
- type sound on or sound off for global sound
- type music on/off for background music only
- type sfx on/off for blip effects only

If game is over:

- use reset to start fresh
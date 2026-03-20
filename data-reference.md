---
layout: page
title: Data Reference
permalink: /data-reference/
nav_exclude: true
---

This page is generated from `_data/tables.json`.
This is the active schema used by the zine and the companion app.

## Metadata

- Title: {{ site.data.tables.game_metadata.title }}
- Schema version: {{ site.data.tables.schema_version }}
- Jam prompt: {{ site.data.tables.game_metadata.jam_prompt }}

## Core Stats (Start)

{% for stat in site.data.tables.character.vital_signs %}
- {{ stat.label }}: {{ stat.start }}
{% endfor %}

## Rule Constants

- Event rolls per loop: {{ site.data.tables.rules.loop.event_rolls_per_loop }}
- Probability threshold: {{ site.data.tables.rules.probability.threshold_percent }}%
- Threshold effect: Stability {{ site.data.tables.rules.probability.threshold_effect.stability_delta }}, SIP +{{ site.data.tables.rules.probability.threshold_effect.sip_delta }}
- Compliance restore: Battery {{ site.data.tables.rules.stability_maintenance.compliance_restore.battery_delta }}, Stability +{{ site.data.tables.rules.stability_maintenance.compliance_restore.stability_delta }}
- Battery hard stop: {{ site.data.tables.rules.battery.hard_stop_at_zero }}

## Phases

{% for phase in site.data.tables.rules.loop.phases %}
- {{ phase.order }}. {{ phase.name }}
{% endfor %}

## Event Categories

| Category | Default Probability | Battery Delta | Stability Delta |
| --- | --- | --- | --- |
{% for category in site.data.tables.random_events.categories %}
| {{ category.id }} | {{ category.default_probability }} | {{ category.default_battery_delta }} | {{ category.default_stability_delta }} |
{% endfor %}

## Random Events (Sample)

| Roll | Prompt | Category | Probability |
| --- | --- | --- | --- |
{% for event in site.data.tables.random_events.events limit: 20 %}
| {{ event.roll }} | {{ event.prompt }} | {{ event.category }} | {{ event.default_probability }} |
{% endfor %}

## Lore Seed

{{ site.data.tables.lore.world_frame.system }}

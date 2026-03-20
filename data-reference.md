---
layout: page
title: Data Reference (Live from JSON)
permalink: /data-reference/
---

This page is generated from _data/tables.json.

If this page changes, the underlying game data changed.

## Core Rules

| Rule | Value |
| --- | --- |
| DC | {{ site.data.tables.core_rules.dc }} |
| Battery cost per objective | {{ site.data.tables.core_rules.objective_battery_cost }} |
| Stability step per player die | {{ site.data.tables.core_rules.stability_step_per_die }} |
| Exhaustion divisor | {{ site.data.tables.core_rules.exhaustion_divisor }} |
| Exhaustion applies to | {{ site.data.tables.core_rules.exhaustion_applies_to | join: ", " }} |
| Recharge roll | {{ site.data.tables.core_rules.recharge_roll }} |
| Recharge rule | {{ site.data.tables.core_rules.recharge_rule }} |
| Loop reset mode | {{ site.data.tables.core_rules.loop_reset_mode }} |
| Loop break condition | {{ site.data.tables.core_rules.loop_break_condition }} |

## SIP Rules

| Rule | Value |
| --- | --- |
| Start SIP | {{ site.data.tables.sip_rules.start }} |
| Gain per completed loop | {{ site.data.tables.sip_rules.gain_per_completed_loop }} |
| Negates Goddess roll | {{ site.data.tables.sip_rules.negates_goddess_roll }} |
| Persists across loops | {{ site.data.tables.sip_rules.persists_across_loops }} |

## Goddess Table

| Stability Range | Die | Effect |
| --- | --- | --- |
{% for row in site.data.tables.goddess_table %}
| {{ row.min_stability }}-{{ row.max_stability }} | {{ row.die }} | {{ row.effect }} |
{% endfor %}

## Seasons and Objectives

{% assign ordered_seasons = site.data.tables.seasons | sort: "order" %}
{% for season in ordered_seasons %}
### {{ season.label }}

| Objective Key | Symbol | Name | Default Pool | Pool Options | Check Type |
| --- | --- | --- | --- | --- | --- |
{% for objective_id in season.objectives %}
{% assign objective = site.data.tables.objective_catalog[objective_id] %}
| {{ objective_id }} | {{ objective.symbol }} | {{ objective.name }} | {{ objective.default_pool | default: "n/a" }} | {{ objective.pool_options | join: ", " | default: "n/a" }} | {{ objective.special_check | default: "standard" }} |
{% endfor %}

{% for objective_id in season.objectives %}
{% assign objective = site.data.tables.objective_catalog[objective_id] %}
{% if objective.prompts %}
#### {{ objective.symbol }} - {{ objective.name }} Prompts ({{ objective.prompt_die }})

| Roll | Prompt |
| --- | --- |
{% for prompt in objective.prompts %}
| {{ forloop.index }} | {{ prompt }} |
{% endfor %}

{% endif %}
{% endfor %}

{% endfor %}

## Result Check (Interview)

{% assign result_obj = site.data.tables.objective_catalog.IN_R %}

- Key: IN_R
- Check: {{ result_obj.special_check }}
- Mode: {{ result_obj.result_check_mode }}
- Rule: {{ result_obj.rules_text }}

## Return Special Checks

{% assign recharge_obj = site.data.tables.objective_catalog.RT_H %}
{% assign receipt_obj = site.data.tables.objective_catalog.RT_I %}

- {{ recharge_obj.symbol }} {{ recharge_obj.name }}: {{ recharge_obj.rules_text }}
- {{ receipt_obj.symbol }} {{ receipt_obj.name }}: {{ receipt_obj.rules_text }}

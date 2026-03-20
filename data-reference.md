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
| Negates The OS roll | {{ site.data.tables.sip_rules.negates_os_roll }} |
| Persists across loops | {{ site.data.tables.sip_rules.persists_across_loops }} |

## The OS Table

| Stability Range | Die | Effect |
| --- | --- | --- |

{% for row in site.data.tables.os_table %}
| {{ row.min_stability }}-{{ row.max_stability }} | {{ row.die }} | {{ row.effect }} |
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

## Architecture of Success

{% assign success_tables = site.data.tables.random_flavor_tables.architecture_of_success %}

- Die: {{ success_tables.die }}
- Rule: {{ success_tables.description }}

| Roll | MSK (The Mask) | SNS (The Senses) | LOG (The Logic) |
| --- | --- | --- | --- |
{% for idx in (0..11) %}
| {{ idx | plus: 1 }} | {{ success_tables.tables.msk[idx] }} | {{ success_tables.tables.sns[idx] }} | {{ success_tables.tables.log[idx] }} |
{% endfor %}

## The Big Book of Glitches

{% assign glitches = site.data.tables.random_flavor_tables.big_book_of_glitches %}

- Die: {{ glitches.die }}
- Trigger: {{ glitches.trigger }}
- Stability penalty: -{{ glitches.stability_penalty }}

| Roll | Glitch |
| --- | --- |
{% for entry in glitches.entries %}
| {{ forloop.index }} | {{ entry }} |
{% endfor %}

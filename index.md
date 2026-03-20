---
layout: page
title: 31st of February
permalink: /
---

A solo glitch-loop RPG.

The date never changes. The interview never ends. Your goal is to lower Stability to 0% and break out.

## Start Here

- [Character Creation](character-creation/)
- [Printable Character Sheet](character-sheet/)
- [Core Mechanics](mechanics/)
- [Stations and Tables](stations/)
- [Play Example](play-example/)
- [Lore](lore/)
- [Game Tables Spec](tables-spec/)
- [Data Reference (Live from JSON)](data-reference/)

## Current Project Status

- Web zine is the source of truth for rules and tables.
- Companion program will use embedded data from these pages.
- Physical zine is a post-jam output from this markdown content.

## Run Locally (Jekyll)

1. Install Ruby and Bundler.
2. In this repository, run `bundle install`.
3. Start the site with `bundle exec jekyll serve`.
4. Open `http://127.0.0.1:4000`.

## Deploy Checklist (GitHub Pages)

1. Push the repo to GitHub.
2. In repo settings, enable Pages for the default branch.
3. Confirm the site URL builds and pages load.
4. Verify links to `character-sheet`, `tables-spec`, and `stations`.
5. Verify `_data/tables.json` matches the current rules text.

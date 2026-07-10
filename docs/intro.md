---
sidebar_position: 1
slug: /
title: Introduction
---

# IntelliKeep

IntelliKeep is a free, open-source custom integration for Home Assistant that keeps track of your home maintenance tasks. It gathers everything in one place, from filter replacements to yearly check-ups, and reminds you before things fall due. Every task keeps its own history, so you always know what was done and when.

## What IntelliKeep does

- Create one-time or recurring tasks (daily, weekly, monthly, yearly, or a custom interval)
- Set a priority (low, medium, high, critical) with color-coded indicators
- Link tasks to Home Assistant areas or specific devices
- Add timestamped notes and keep track of who wrote them
- Keep an activity log of every edit, completion, and reopen
- View tasks on a calendar (week or month) filtered by area, device, and priority
- Browse the full execution history, with CSV export and print support
- Get notifications through HA persistent notifications or optional mobile push
- Watch task state through three sensor entities: `tasks_due_today`, `tasks_overdue`, `next_due_task`
- Show due and overdue tasks on your dashboard with the Lovelace card

## What IntelliKeep does not do

- Automatic device discovery
- Vendor firmware updates
- External account authentication or syncing with third-party task platforms

## Quick start

1. [Install via HACS](./installation/hacs) (recommended)
2. Restart Home Assistant
3. Add the integration under **Settings → Devices & Services**
4. Open the IntelliKeep panel in the sidebar and create your first task

---
sidebar_position: 1
slug: /
title: Introduction
---

# IntelliKeep

**IntelliKeep** is a home maintenance task management system built as a free, open-source custom integration for Home Assistant. It centralizes all your household tasks — from simple filter replacements to periodic check-ups — offering automatic alerts and a complete task history.

## What IntelliKeep does

- Create **one-time or recurring tasks** (daily, weekly, monthly, yearly, or custom interval)
- Set **priority levels** (low, medium, high, critical) with color-coded visual indicators
- Link tasks to **Home Assistant areas or specific devices**
- Add **timestamped notes** with author tracking per task
- Track a full **activity log** for every edit, completion, and reopen
- View tasks in a **Calendar** (week/month) with area, device, and priority filters
- Browse a complete **Execution History** with CSV export and print support
- Receive **notifications** via HA persistent notifications or optional mobile push
- Monitor task state via three **sensor entities**: `tasks_due_today`, `tasks_overdue`, `next_due_task`
- Display due and overdue tasks on your HA dashboard using the **Lovelace card**

## What IntelliKeep does not do

- Automatic device discovery
- Vendor firmware updates
- External account authentication or sync with third-party task platforms

## Quick start

1. [Install via HACS](./installation/hacs) (recommended)
2. Restart Home Assistant
3. Add the integration under **Settings → Devices & Services**
4. Open the **IntelliKeep panel** in the HA sidebar and create your first task

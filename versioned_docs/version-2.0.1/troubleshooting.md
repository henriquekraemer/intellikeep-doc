---
sidebar_position: 8
title: Troubleshooting
---

# Troubleshooting

## Panel or card not showing current data

1. Go to **Settings → Devices & Services** and confirm the IntelliKeep entry is loaded and shows no errors
2. Download **Diagnostics** from the config entry and check that the task counters look right
3. If you just updated IntelliKeep, **restart Home Assistant** and reload the browser page (clear its cache if needed) to load the new frontend files

## "Custom element doesn't exist: intellikeep-card"

The dashboard can't find the card's code.

1. If your dashboards are configured in YAML, add the card resource by hand, as described in [YAML-mode dashboards](./lovelace-card#yaml-mode-dashboards)
2. Otherwise, check under **Settings → Dashboards → ⋮ → Resources** that `/intellikeep_static/intellikeep-card.js` is listed, restart Home Assistant and reload the page

## Mobile notifications not delivered

1. In **Settings → Tools → Actions** (**Developer tools → Actions** in older Home Assistant versions), check that the `notify.*` service you configured actually exists
2. Leave the **Notification Service** field empty to fall back to persistent notifications only
3. Check the **Home Assistant logs** for IntelliKeep errors (filter by `intellikeep`)
4. Remember that each task is notified once per stage until Home Assistant restarts

## Tasks appear overdue unexpectedly

1. Check the Home Assistant **time zone** under **Settings → System → Home information** (**General** in older versions). Tasks fall due and become overdue at midnight in that time zone
2. Check the time zone of your **user profile**: dates in the panel follow it
3. Confirm the stored `due_date` value in the task's diagnostics
4. Open the task's **History** tab to see whether it was completed and then reopened

## A recurring task got an unexpected next date

1. Check **Count the next due date from** in the task dialog. With **Completion date**, a late completion also moves the next occurrence; with **Original due date**, the task keeps a fixed calendar
2. For weekly tasks with days selected, the next occurrence is the next selected day after the current due date, at the task's original time
3. Dates in the panel's Calendar tab for future repeats are an estimate for tasks counted from completion

## Integration fails to load after an update

1. Check the logs for Python errors related to `custom_components.intellikeep`
2. Make sure the whole `custom_components/intellikeep/` directory was replaced, not just some files
3. If you use HACS, download the integration again and restart
4. Check that Home Assistant is 2026.1 or later

## Known limitations

- IntelliKeep is single-instance: only one integration entry is allowed per Home Assistant installation
- Task data is stored locally (in `.storage/intellikeep`) and is not shared between Home Assistant installations
- Tasks are not individual entities: the sensors summarize them, and the to-do list and the calendar list them
- The `calendar.intellikeep_tasks` entity shows only the current occurrence of each recurring task. The panel's Calendar tab projects the next ones, and for tasks counted from completion those dates are an estimate
- Notification deduplication is kept in memory and resets when Home Assistant restarts

## Removing IntelliKeep

1. Go to **Settings → Devices & Services**
2. Open **IntelliKeep** and choose **Delete**
3. Remove any dashboard cards or automations that still use IntelliKeep actions, entities or events
4. If you installed it manually, delete `custom_components/intellikeep/` from your Home Assistant config directory

---
sidebar_position: 8
title: Troubleshooting
---

# Troubleshooting

## Panel or card not showing current data

1. Go to **Settings → Devices & Services** and confirm the IntelliKeep entry is loaded and shows no errors
2. Download **Diagnostics** from the config entry and verify the task counters match expectations
3. If you recently rebuilt or updated the frontend, **restart Home Assistant** to reload the static assets

## Mobile notifications not delivered

1. In **Developer Tools → Actions**, verify the `notify.*` service you configured actually exists
2. Leave the **Notification Service** field empty to fall back to persistent HA notifications only
3. Check **Home Assistant logs** for IntelliKeep-related errors (filter by `intellikeep`)

## Tasks appear overdue unexpectedly

1. Check the Home Assistant **system time and timezone** — IntelliKeep uses HA system time
2. Confirm the stored `due_date` value in the task's diagnostics
3. Open the task's **Activity Log** to see whether it was completed and then reopened

## Integration fails to load after update

1. Clear the browser cache and reload
2. Check logs for Python import errors related to `custom_components.intellikeep`
3. Ensure the entire `custom_components/intellikeep/` directory was replaced (not just some files)
4. If using HACS, re-download the integration and restart

## Known limitations

- IntelliKeep is **single-instance** — only one integration entry per Home Assistant instance
- Task data is stored locally and is not shared between HA instances
- Notification deduplication is in-memory and **resets after an HA restart**
- Sensors summarize task state; individual task entities are not created

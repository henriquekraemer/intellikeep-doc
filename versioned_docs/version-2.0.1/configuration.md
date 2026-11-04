---
sidebar_position: 3
title: Configuration
---

# Configuration

## Initial setup

During the integration setup wizard you can configure:

| Option | Default | Description |
|---|---|---|
| **Instance Name** | `IntelliKeep` | Name of the IntelliKeep device in Home Assistant. Entity IDs are built from it |
| **Default Notification Lead Time (days)** | `1` | How many days before the due date a reminder is sent (0–30). New tasks start with this value, and each task can change it |
| **Notification Service** | *(empty)* | Optional `notify.*` service, for example `notify.mobile_app_my_phone` |

Only one IntelliKeep instance can be set up per Home Assistant installation.

## Changing settings later

All options can be changed after installation:

1. Go to **Settings → Devices & Services**
2. Find the **IntelliKeep** entry
3. Click **Configure** to adjust the settings, or choose **Reconfigure** from the ⋮ menu to run the setup wizard again

IntelliKeep reloads once with the new settings.

## Notification service

Leave **Notification Service** empty if you only want Home Assistant persistent notifications (the bell icon in the UI).

To also get mobile push notifications, enter a `notify.*` service name. You can find the services available in your installation under **Settings → Tools → Actions** (**Developer tools → Actions** in older Home Assistant versions).

Example values:
- `notify.mobile_app_my_phone`
- `notify.all_devices`

See [Notifications & Sensors](./features/notifications) for when reminders are sent.

## Entity IDs

IntelliKeep creates one device, named after the **Instance Name**, with these entities:

| Entity | Description |
|---|---|
| `sensor.intellikeep_tasks_due_today` | Tasks due today or already overdue |
| `sensor.intellikeep_tasks_overdue` | Overdue tasks |
| `sensor.intellikeep_next_due_task` | The next task to fall due |
| `todo.intellikeep_tasks` | [To-do list](./features/todo-and-calendar#to-do-list) with the open and recently completed tasks |
| `calendar.intellikeep_tasks` | [Calendar](./features/todo-and-calendar#calendar) with the open tasks on their due dates |

The IDs above assume the default instance name. With a different name, the `intellikeep` part follows it (for example, `todo.home_tasks` for an instance called *Home*).

## Language, dates and times

The panel and the dashboard card follow the language set in your Home Assistant user profile (English, Portuguese and Spanish are available, with English as the fallback). Dates and times follow the profile's language, time zone, first day of the week and 12/24-hour clock.

Tasks fall due and become overdue at local midnight, in Home Assistant's time zone.

## Panel settings

The gear icon in the panel header opens the panel's own settings:

- **Task animations**: turn the transitions off when completing, deleting, reopening or moving between tasks. This is saved per browser.
- **Delete all data**: permanently deletes every task, note and completion record. It asks for confirmation and needs an admin user.

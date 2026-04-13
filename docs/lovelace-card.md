---
sidebar_position: 5
title: Lovelace Card
---

# Lovelace Card

IntelliKeep includes a custom Lovelace card for compact dashboard display of due and overdue tasks.

## Adding the card

In your Home Assistant dashboard, add a new card and choose **Custom: IntelliKeep Card**. Or add it manually in YAML mode:

```yaml
type: custom:intellikeep-card
title: IntelliKeep
max_tasks: 5
show_linked_entities: true
show_description: false
```

## Configuration options

| Option | Type | Default | Description |
|---|---|---|---|
| `title` | string | `IntelliKeep` | Card title displayed in the header |
| `max_tasks` | number | `5` | Maximum number of tasks to display |
| `show_linked_entities` | boolean | `true` | Show the linked area/device label on each task |
| `show_description` | boolean | `false` | Show the task description text |
| `filter_priority` | list | — | Only show tasks with these priorities: `low`, `medium`, `high`, `critical` |
| `filter_status` | list | — | Only show tasks with these statuses: `pending`, `due`, `overdue`, `completed`, `snoozed` |

## Display

The card shows tasks sorted by urgency (overdue first, then by due date). Each task row displays:
- Priority color bar
- Task name
- Due date (or "Overdue" label)
- Linked entity (if `show_linked_entities: true`)

Clicking a task row opens the full task detail in the IntelliKeep panel.

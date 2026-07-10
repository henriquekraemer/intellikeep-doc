---
sidebar_position: 5
title: Lovelace Card
---

# Lovelace Card

IntelliKeep ships with a custom Lovelace card that shows due and overdue tasks in a compact form on your dashboard.

## Adding the card

On your Home Assistant dashboard, add a new card and pick **Custom: IntelliKeep Card**. You can also add it by hand in YAML mode:

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

The card sorts tasks by urgency, with overdue ones first and the rest by due date. Each row shows:
- Priority color bar
- Task name
- Due date, or an "Overdue" label
- Linked entity, when `show_linked_entities` is `true`

Clicking a row opens the full task detail in the IntelliKeep panel.

---
sidebar_position: 3
title: Upgrading from 1.x
---

# Upgrading from 1.x

IntelliKeep 2.0 redesigned the panel and the dashboard card, and a few things work differently from 1.x. Most installs need no changes, but check the list below before you update.

:::warning Back up first
Back up Home Assistant before updating. Stored tasks are converted on the first start of 2.x, and going back to 1.x afterwards is not supported.
:::

## What may need your attention

### The dashboard card shows fewer tasks

The card now lists **3 tasks** by default instead of 10, and it leaves completed tasks out. To keep the old behavior, add these options to the card:

```yaml
type: custom:intellikeep-card
max_tasks: 10
filter_status: [pending, due, overdue, completed]
```

See [Lovelace Card](../lovelace-card) for every option.

### Reopening a task undoes the completion

`intellikeep.reopen_task` now takes the completion back: its record leaves the history, and the next occurrence that the completion created for a recurring task is removed, unless someone already edited it, added a note to it or completed it. In 1.x, reopening a recurring task left two open occurrences.

Check any automation that reopens tasks.

### `frequency: custom` is stored as `daily`

The old **custom** frequency with `custom_days_interval` is now a daily task with a [`repeat_interval`](../features/tasks#recurring-tasks). Existing tasks are converted when IntelliKeep loads, and actions that still send `frequency: custom` keep working.

However, the `next_due_task` sensor and the panel now report `daily`, so templates that compare the frequency with `custom` need updating.

### 1.x ignores the new task fields

If you go back to 1.x anyway, the fields added in 2.0 are ignored: a task that repeats every 3 days would repeat every day, and a task counted from its due date would count from the completion again.

## What's new in 2.0

- A redesigned panel: tasks grouped by due date, priority or area, a checkbox with Undo, and a ⋮ menu with Edit, Duplicate, History and Delete
- Tasks that repeat every N days, weeks, months or years, counted from the completion or from the due date
- An icon per task
- A to-do list entity and a calendar entity for Home Assistant's own To-do lists and Calendar
- Future repeats of recurring tasks in the panel's Calendar tab
- A new History tab with who completed each task and whether it was on time
- A redesigned dashboard card with a checkbox per task

The full list is in the [changelog](https://github.com/henriquekraemer/intellikeep/blob/main/CHANGELOG.md).

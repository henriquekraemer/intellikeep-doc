---
sidebar_position: 6
title: Services
---

# Services

IntelliKeep provides the Home Assistant actions below. You can call them from automations, scripts, or **Settings → Tools → Actions** (**Developer tools → Actions** in older Home Assistant versions). The action editor shows the actions, their fields and their options in the language of your profile (English, Portuguese or Spanish).

Task IDs appear in the attributes of the [sensors](./features/notifications#sensor-entities), in the [events](./features/notifications#notification-event) and in diagnostics.

## `intellikeep.create_task`

Create a new task.

```yaml
action: intellikeep.create_task
data:
  name: Replace HVAC filter
  icon: mdi:air-filter
  priority: high
  frequency: monthly
  repeat_interval: 3
  schedule_anchor: due_date
  due_date: "2026-12-01T09:00:00"
  linked_entity_ids:
    - area:living_room          # link to an area
    - device:abc123def456       # or a specific device ID
  notify_days_before: 3
  notify_on_overdue: true
```

| Field | Required | Default | Description |
|---|---|---|---|
| `name` | Yes | — | Task name |
| `description` | No | — | Free-text description |
| `icon` | No | `mdi:wrench-outline` | Icon shown next to the task, e.g. `mdi:air-filter` |
| `priority` | No | `medium` | `low`, `medium`, `high` or `critical` |
| `frequency` | No | `one_time` | `one_time`, `daily`, `weekly`, `monthly` or `yearly`. For recurring tasks, it is the unit of `repeat_interval` |
| `repeat_interval` | No | `1` | Repeats every N days, weeks, months or years (1–3650) |
| `schedule_anchor` | No | `completion` | What the next due date is counted from: `completion` or `due_date`. See [Recurring tasks](./features/tasks#count-the-next-due-date-from) |
| `weekdays` | No | — | For weekly tasks: the days it repeats on, from `mon` to `sun`, e.g. `[mon, wed, fri]` |
| `due_date` | No | — | ISO 8601 date and time. Without a UTC offset, it is read in Home Assistant's time zone. Midnight makes the task all day |
| `linked_entity_ids` | No | — | Areas (`area:<area_id>`) and devices (`device:<device_id>`) to link the task to |
| `notify_days_before` | No | Integration default | Days before the due date to send a reminder (0–365) |
| `notify_on_overdue` | No | `true` | Send a notification when the task becomes overdue |

### Examples

A weekly task on specific days. The next occurrence is always the next selected day, at the same time, so the schedule doesn't drift when a task is completed late:

```yaml
action: intellikeep.create_task
data:
  name: Take out the garbage
  icon: mdi:trash-can-outline
  frequency: weekly
  weekdays: [mon, wed, fri]
  due_date: "2026-11-09T07:00:00"
```

A task every 10 days, counted from each completion:

```yaml
action: intellikeep.create_task
data:
  name: Clean the coffee machine
  frequency: daily
  repeat_interval: 10
```

:::note Legacy `custom` frequency
`frequency: custom` with `custom_days_interval` from versions before 2.0 still works. It is stored as `frequency: daily` with that `repeat_interval`.
:::

## `intellikeep.complete_task`

Mark a task as done and record a completion. For recurring tasks, the next occurrence is created.

```yaml
action: intellikeep.complete_task
data:
  task_id: "<task_id>"
  completed_by: "Henrique"
  notes: "Replaced with a MERV-13 filter."
```

| Field | Required | Description |
|---|---|---|
| `task_id` | Yes | ID of the task to complete |
| `completed_by` | No | Name of who completed the task, shown in the history |
| `notes` | No | Completion notes |

## `intellikeep.reopen_task`

Reopen a completed task, setting it back to open. The completion is undone: its record leaves the history, and for a recurring task the next occurrence it created is removed, unless it was already edited, noted or completed.

```yaml
action: intellikeep.reopen_task
data:
  task_id: "<task_id>"
  performed_by: "Henrique"
```

| Field | Required | Description |
|---|---|---|
| `task_id` | Yes | ID of the task to reopen |
| `performed_by` | No | Name of who reopened the task, shown in the activity log |

## `intellikeep.update_task`

Update fields of an existing task. Only the fields you send are changed, and the change is recorded in the task's activity log.

```yaml
action: intellikeep.update_task
data:
  task_id: "<task_id>"
  priority: critical
  due_date: "2026-12-15T09:00:00"
  updated_by: "Henrique"
```

Accepts the same fields as [`create_task`](#intellikeepcreate_task), plus:

| Field | Required | Description |
|---|---|---|
| `task_id` | Yes | ID of the task to update |
| `enabled` | No | `false` closes the task without recording a completion, `true` opens it again. To complete a task, use [`complete_task`](#intellikeepcomplete_task) |
| `updated_by` | No | Name of who made the change, shown in the activity log |

## `intellikeep.delete_task`

Permanently delete a task, with its notes and history.

```yaml
action: intellikeep.delete_task
data:
  task_id: "<task_id>"
```

| Field | Required | Description |
|---|---|---|
| `task_id` | Yes | ID of the task to delete |

## `intellikeep.add_task_note`

Add a timestamped note to a task.

```yaml
action: intellikeep.add_task_note
data:
  task_id: "<task_id>"
  content: "Noticed some wear on the belt. Check again next month."
  added_by: "Henrique"
```

| Field | Required | Description |
|---|---|---|
| `task_id` | Yes | ID of the task to add the note to |
| `content` | Yes | Text of the note |
| `added_by` | No | Name of who added the note |

## `intellikeep.delete_task_note`

Delete a note from a task.

```yaml
action: intellikeep.delete_task_note
data:
  task_id: "<task_id>"
  note_id: "<note_id>"
```

| Field | Required | Description |
|---|---|---|
| `task_id` | Yes | ID of the task that owns the note |
| `note_id` | Yes | ID of the note to delete |

## `intellikeep.load_sample_data`

Add a set of sample home maintenance tasks, with icons. Useful for exploring the panel after a fresh install.

```yaml
action: intellikeep.load_sample_data
```

## `intellikeep.delete_all_data`

Permanently delete every task, note and completion record. Only admin users can call this action.

```yaml
action: intellikeep.delete_all_data
```

:::danger
This action can't be undone. All task data is permanently removed.
:::

## To-do actions

The [to-do list](./features/todo-and-calendar#to-do-list) also accepts Home Assistant's `todo.*` actions, such as `todo.add_item`, `todo.update_item` and `todo.remove_item`, on `todo.intellikeep_tasks`.

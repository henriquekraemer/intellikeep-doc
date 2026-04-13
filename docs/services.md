---
sidebar_position: 6
title: Services
---

# Services

IntelliKeep exposes the following Home Assistant service actions. Use them in automations, scripts, or the Developer Tools → Actions panel.

## `intellikeep.create_task`

Create a new task.

```yaml
action: intellikeep.create_task
data:
  name: Replace HVAC filter
  priority: high
  frequency: monthly
  due_date: "2025-02-01T09:00:00"
  linked_entity_ids:
    - sensor.hvac_filter
  notify_days_before: 3
  notify_on_overdue: true
```

| Field | Required | Default | Description |
|---|---|---|---|
| `name` | Yes | — | Task name |
| `description` | No | — | Free-text description |
| `priority` | No | `medium` | `low`, `medium`, `high`, `critical` |
| `frequency` | No | `one_time` | `one_time`, `daily`, `weekly`, `monthly`, `yearly`, `custom` |
| `custom_days_interval` | No | — | Days between occurrences when `frequency` is `custom` |
| `due_date` | No | — | ISO 8601 datetime string |
| `linked_entity_ids` | No | — | List of HA entity IDs to associate with the task |
| `notify_days_before` | No | `1` | Days before due date to send a reminder |
| `notify_on_overdue` | No | `true` | Send a notification when the task becomes overdue |

## `intellikeep.complete_task`

Mark a task as done and record an execution entry. For recurring tasks, the next occurrence is automatically scheduled.

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
| `completed_by` | No | Name or identifier of who completed the task |
| `notes` | No | Optional completion notes |

## `intellikeep.reopen_task`

Reopen a completed task, marking it as pending again.

```yaml
action: intellikeep.reopen_task
data:
  task_id: "<task_id>"
```

## `intellikeep.update_task`

Update fields of an existing task. Only the fields provided are changed.

```yaml
action: intellikeep.update_task
data:
  task_id: "<task_id>"
  priority: critical
  due_date: "2025-03-01T09:00:00"
  updated_by: "Henrique"
```

Accepts the same fields as `create_task`, plus:

| Field | Required | Description |
|---|---|---|
| `task_id` | Yes | ID of the task to update |
| `enabled` | No | Enable or disable the task (`true` / `false`) |
| `updated_by` | No | Name or identifier of who made the update |

## `intellikeep.delete_task`

Permanently delete a task and its history.

```yaml
action: intellikeep.delete_task
data:
  task_id: "<task_id>"
```

## `intellikeep.add_task_note`

Add a timestamped note to an existing task.

```yaml
action: intellikeep.add_task_note
data:
  task_id: "<task_id>"
  content: "Noticed some wear on the belt — monitor next month."
  added_by: "Henrique"
```

| Field | Required | Description |
|---|---|---|
| `task_id` | Yes | ID of the task to add the note to |
| `content` | Yes | Text content of the note |
| `added_by` | No | Name or identifier of who added the note |

## `intellikeep.delete_task_note`

Delete a specific note from a task.

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

## `intellikeep.delete_all_data`

Permanently delete all tasks, notes, and execution history.

```yaml
action: intellikeep.delete_all_data
```

:::danger
This action is irreversible. All task data will be permanently removed.
:::

## `intellikeep.load_sample_data`

Populate IntelliKeep with sample home maintenance tasks. Useful for exploring the UI after a fresh install.

```yaml
action: intellikeep.load_sample_data
```

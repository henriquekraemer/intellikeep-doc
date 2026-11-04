---
sidebar_position: 5
title: Notifications & Sensors
---

# Notifications & Sensors

## Notifications

IntelliKeep reminds you as tasks approach their due date, and again once they are overdue.

### How notifications work

- Checks run once an hour
- A reminder goes out when a task is within its **Remind me** window: N days before the due date, set per task (new tasks start with the default from the [integration options](../configuration))
- An overdue task gets its own notification, unless **Notify when overdue** is off for it
- Each task is notified once per stage. This deduplication is kept in memory, so it resets when Home Assistant restarts
- Completing or deleting a task clears its notification state

### Notification channels

| Channel | Always active | How to configure |
|---|---|---|
| Home Assistant persistent notifications | Yes | Built in, no configuration needed |
| Mobile push (or any `notify.*` service) | Optional | Set a notification service in [Configuration](../configuration#notification-service) |

### Notification event

Every notification also fires an `intellikeep_task_notification` event that you can use in automations:

```yaml
triggers:
  - trigger: event
    event_type: intellikeep_task_notification
    event_data:
      event_type: overdue   # or "approaching"
```

| Field | Description |
|---|---|
| `event_type` | `approaching` or `overdue` |
| `task_id` | ID of the task |
| `title` | Notification title |
| `message` | Notification message |
| `notification_id` | ID of the persistent notification |

### Task update event

IntelliKeep also fires `intellikeep_task_updated` whenever a task changes, with the fields `task_id` and `action`. The action is one of `created`, `updated`, `completed`, `reopened`, `deleted`, `note_added` or `note_deleted`.

```yaml
triggers:
  - trigger: event
    event_type: intellikeep_task_updated
    event_data:
      action: completed
```

See [Automations](../automations) for complete examples.

## Sensor entities

IntelliKeep creates three sensors that you can use in dashboards and automations:

| Entity | State | Attributes |
|---|---|---|
| `sensor.intellikeep_tasks_due_today` | Number of open tasks due today or already overdue | — |
| `sensor.intellikeep_tasks_overdue` | Number of overdue tasks | `overdue_tasks`: list with the `task_id`, `name`, `due_date` and `priority` of each overdue task |
| `sensor.intellikeep_next_due_task` | Name of the open task with the nearest due date | `task_id`, `due_date`, `priority`, `linked_entity_ids`, `frequency`, `repeat_interval`, `weekdays` |

The entity IDs assume the default instance name; see [Entity IDs](../configuration#entity-ids).

IntelliKeep also has a [to-do list and a calendar entity](./todo-and-calendar).

## Data updates

Task state is refreshed:

- Right after any change made from the panel, the card, the to-do list or an action
- Every 5 minutes, so the counts follow the clock (a task becomes due or overdue at local midnight)
- The panel and the card receive updates as soon as the data changes, without reloading the page

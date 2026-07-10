---
sidebar_position: 4
title: Notifications & Sensors
---

# Notifications & Sensors

## Notifications

IntelliKeep sends reminders as tasks approach their due date, and again once they are overdue.

### How notifications work

- Checks run once an hour
- A reminder goes out N days before the due date (set globally, or per task)
- Overdue tasks trigger their own notification
- Deduplication is kept in memory and resets when Home Assistant restarts

### Notification channels

| Channel | Always active | How to configure |
|---|---|---|
| HA persistent notifications | Yes | Built-in, no config needed |
| Mobile push | Optional | Set a `notify.*` service in [Configuration](../configuration) |

### Automation trigger

IntelliKeep fires an event you can use in HA automations:

```yaml
triggers:
  - trigger: event
    event_type: intellikeep_task_notification
    event_data:
      event_type: overdue   # or "approaching"
```

Available event data fields: `task_id`, `title`, `message`, `event_type`.

## Sensor entities

IntelliKeep creates three sensor entities that you can use in dashboards and automations:

| Entity | Description |
|---|---|
| `sensor.intellikeep_tasks_due_today` | Number of tasks due today |
| `sensor.intellikeep_tasks_overdue` | Number of currently overdue tasks |
| `sensor.intellikeep_next_due_task` | Name and due date of the next upcoming task |

Sensor state is refreshed:
- Right after any service action that changes task data
- Every 5 minutes through the scheduled coordinator refresh

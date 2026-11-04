---
sidebar_position: 7
title: Automations
---

# Automations

IntelliKeep works with Home Assistant automations through its events, sensors, calendar and to-do list, and its actions can be called from any automation or script.

## Notify on an overdue task

```yaml
automation:
  alias: Notify on overdue IntelliKeep task
  triggers:
    - trigger: event
      event_type: intellikeep_task_notification
      event_data:
        event_type: overdue
  actions:
    - action: notify.mobile_app_my_phone
      data:
        title: "{{ trigger.event.data.title }}"
        message: "{{ trigger.event.data.message }}"
```

## Notify when a task is approaching its due date

```yaml
automation:
  alias: Notify when a task is approaching its due date
  triggers:
    - trigger: event
      event_type: intellikeep_task_notification
      event_data:
        event_type: approaching
  actions:
    - action: notify.mobile_app_my_phone
      data:
        title: "{{ trigger.event.data.title }}"
        message: "{{ trigger.event.data.message }}"
```

## Remind me when a task becomes due

The [calendar entity](./features/todo-and-calendar#calendar) fires calendar triggers at each task's due time (all-day tasks at midnight):

```yaml
automation:
  alias: Remind me when a maintenance task is due
  triggers:
    - trigger: calendar
      event: start
      entity_id: calendar.intellikeep_tasks
  actions:
    - action: notify.mobile_app_my_phone
      data:
        title: Maintenance due
        message: "{{ trigger.calendar_event.summary }}"
```

## React when a task is completed

`intellikeep_task_updated` fires on every change to a task. This example announces completions:

```yaml
automation:
  alias: Announce completed maintenance
  triggers:
    - trigger: event
      event_type: intellikeep_task_updated
      event_data:
        action: completed
  actions:
    - action: notify.mobile_app_my_phone
      data:
        title: IntelliKeep
        message: "A maintenance task was completed ({{ trigger.event.data.task_id }})."
```

## Alert when too many tasks are overdue

```yaml
automation:
  alias: Alert when more than 3 tasks are overdue
  triggers:
    - trigger: numeric_state
      entity_id: sensor.intellikeep_tasks_overdue
      above: 3
  actions:
    - action: notify.mobile_app_my_phone
      data:
        title: IntelliKeep
        message: "You have {{ states('sensor.intellikeep_tasks_overdue') }} overdue maintenance tasks."
```

## Create a task from a device state

Create a one-time task when a sensor says something needs attention, for example a low battery:

```yaml
automation:
  alias: Replace the smoke detector battery
  triggers:
    - trigger: numeric_state
      entity_id: sensor.smoke_detector_battery
      below: 15
  actions:
    - action: intellikeep.create_task
      data:
        name: Replace the smoke detector battery
        icon: mdi:battery-alert
        priority: high
        due_date: "{{ (now() + timedelta(days=3)).isoformat() }}"
```

## Add a task with a voice assistant

Because `todo.intellikeep_tasks` is a regular to-do list, voice assistants and the `todo.add_item` action can add tasks to it:

```yaml
action: todo.add_item
target:
  entity_id: todo.intellikeep_tasks
data:
  item: Check the water softener salt
  due_date: "2026-11-15"
```

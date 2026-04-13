---
sidebar_position: 7
title: Automations
---

# Automations

IntelliKeep integrates with Home Assistant automations through its sensor entities and notification events.

## Trigger on overdue task notification

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

## Trigger on approaching task notification

```yaml
automation:
  alias: Notify when task is approaching due date
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

## Trigger on sensor threshold

Create a task when the number of overdue tasks exceeds a threshold:

```yaml
automation:
  alias: Alert when more than 3 tasks overdue
  triggers:
    - trigger: numeric_state
      entity_id: sensor.intellikeep_tasks_overdue
      above: 3
  actions:
    - action: notify.mobile_app_my_phone
      data:
        title: "IntelliKeep"
        message: "You have {{ states('sensor.intellikeep_tasks_overdue') }} overdue maintenance tasks."
```

## Create a task from an automation

```yaml
automation:
  alias: Schedule annual boiler service
  triggers:
    - trigger: time
      at: "09:00:00"
  conditions:
    - condition: template
      value_template: "{{ now().month == 9 and now().day == 1 }}"
  actions:
    - action: intellikeep.create_task
      data:
        name: Annual boiler service
        priority: high
        frequency: yearly
        due_date: "{{ (now() + timedelta(days=30)).isoformat() }}"
```

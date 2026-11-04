---
sidebar_position: 7
title: Automatizaciones
---

# Automatizaciones

IntelliKeep funciona con las automatizaciones de Home Assistant a través de sus eventos, sus sensores, su calendario y su lista de tareas pendientes, y sus acciones se pueden llamar desde cualquier automatización o script.

## Notificar una tarea vencida

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

## Notificar cuando una tarea se acerca a su fecha de vencimiento

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

## Recordarme cuando vence una tarea

La [entidad de calendario](./features/todo-and-calendar#calendar) activa los disparadores de calendario a la hora de vencimiento de cada tarea (las tareas de todo el día, a medianoche):

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

## Reaccionar cuando se completa una tarea

`intellikeep_task_updated` se dispara con cada cambio en una tarea. Este ejemplo anuncia las finalizaciones:

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

## Alertar cuando hay demasiadas tareas vencidas

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

## Crear una tarea a partir del estado de un dispositivo

Crea una tarea única cuando un sensor indica que algo necesita atención, por ejemplo una batería baja:

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

## Añadir una tarea con un asistente de voz

Como `todo.intellikeep_tasks` es una lista de tareas pendientes normal, los asistentes de voz y la acción `todo.add_item` pueden añadirle tareas:

```yaml
action: todo.add_item
target:
  entity_id: todo.intellikeep_tasks
data:
  item: Check the water softener salt
  due_date: "2026-11-15"
```

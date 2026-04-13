---
sidebar_position: 7
title: Automatizaciones
---

# Automatizaciones

IntelliKeep se integra con las automatizaciones de Home Assistant mediante sus entidades sensor y eventos de notificación.

## Disparar en notificación de tarea vencida

```yaml
automation:
  alias: Notificar tarea IntelliKeep vencida
  triggers:
    - trigger: event
      event_type: intellikeep_task_notification
      event_data:
        event_type: overdue
  actions:
    - action: notify.mobile_app_mi_telefono
      data:
        title: "{{ trigger.event.data.title }}"
        message: "{{ trigger.event.data.message }}"
```

## Disparar en notificación de tarea próxima a vencer

```yaml
automation:
  alias: Notificar cuando una tarea se aproxima a su vencimiento
  triggers:
    - trigger: event
      event_type: intellikeep_task_notification
      event_data:
        event_type: approaching
  actions:
    - action: notify.mobile_app_mi_telefono
      data:
        title: "{{ trigger.event.data.title }}"
        message: "{{ trigger.event.data.message }}"
```

## Disparar por umbral en sensor

Crear una alerta cuando el número de tareas vencidas supera un umbral:

```yaml
automation:
  alias: Alertar cuando más de 3 tareas estén vencidas
  triggers:
    - trigger: numeric_state
      entity_id: sensor.intellikeep_tasks_overdue
      above: 3
  actions:
    - action: notify.mobile_app_mi_telefono
      data:
        title: "IntelliKeep"
        message: "Tienes {{ states('sensor.intellikeep_tasks_overdue') }} tareas de mantenimiento vencidas."
```

## Crear una tarea desde una automatización

```yaml
automation:
  alias: Programar servicio anual de caldera
  triggers:
    - trigger: time
      at: "09:00:00"
  conditions:
    - condition: template
      value_template: "{{ now().month == 9 and now().day == 1 }}"
  actions:
    - action: intellikeep.create_task
      data:
        name: Servicio anual de caldera
        priority: high
        frequency: yearly
        due_date: "{{ (now() + timedelta(days=30)).isoformat() }}"
```

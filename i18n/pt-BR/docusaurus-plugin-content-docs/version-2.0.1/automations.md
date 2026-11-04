---
sidebar_position: 7
title: Automações
---

# Automações

O IntelliKeep funciona com as automações do Home Assistant por meio dos seus eventos, sensores, calendário e lista de tarefas, e as ações dele podem ser chamadas em qualquer automação ou script.

## Notificar quando uma tarefa fica atrasada

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

## Notificar quando uma tarefa está perto do vencimento

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

## Avisar quando uma tarefa vence

A [entidade de calendário](./features/todo-and-calendar#calendar) dispara gatilhos de calendário no horário de vencimento de cada tarefa (as tarefas de dia inteiro, à meia-noite):

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

## Reagir quando uma tarefa é concluída

`intellikeep_task_updated` dispara a cada mudança em uma tarefa. Este exemplo anuncia as conclusões:

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

## Alertar quando houver tarefas atrasadas demais

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

## Criar uma tarefa a partir do estado de um dispositivo

Crie uma tarefa única quando um sensor indicar que algo precisa de atenção, por exemplo uma bateria fraca:

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

## Adicionar uma tarefa com um assistente de voz

Como `todo.intellikeep_tasks` é uma lista de tarefas comum, os assistentes de voz e a ação `todo.add_item` podem adicionar tarefas a ela:

```yaml
action: todo.add_item
target:
  entity_id: todo.intellikeep_tasks
data:
  item: Check the water softener salt
  due_date: "2026-11-15"
```

---
sidebar_position: 7
title: Automações
---

# Automações

O IntelliKeep se integra com as automações do Home Assistant por meio das suas entidades sensor e eventos de notificação.

## Disparar em notificação de tarefa vencida

```yaml
automation:
  alias: Notificar sobre tarefa IntelliKeep vencida
  triggers:
    - trigger: event
      event_type: intellikeep_task_notification
      event_data:
        event_type: overdue
  actions:
    - action: notify.mobile_app_meu_celular
      data:
        title: "{{ trigger.event.data.title }}"
        message: "{{ trigger.event.data.message }}"
```

## Disparar em notificação de tarefa se aproximando do vencimento

```yaml
automation:
  alias: Notificar quando tarefa estiver próxima do vencimento
  triggers:
    - trigger: event
      event_type: intellikeep_task_notification
      event_data:
        event_type: approaching
  actions:
    - action: notify.mobile_app_meu_celular
      data:
        title: "{{ trigger.event.data.title }}"
        message: "{{ trigger.event.data.message }}"
```

## Disparar por limite no sensor

Criar uma tarefa quando o número de tarefas vencidas ultrapassa um limite:

```yaml
automation:
  alias: Alertar quando mais de 3 tarefas estiverem vencidas
  triggers:
    - trigger: numeric_state
      entity_id: sensor.intellikeep_tasks_overdue
      above: 3
  actions:
    - action: notify.mobile_app_meu_celular
      data:
        title: "IntelliKeep"
        message: "Você tem {{ states('sensor.intellikeep_tasks_overdue') }} tarefas de manutenção vencidas."
```

## Criar uma tarefa a partir de uma automação

```yaml
automation:
  alias: Agendar revisão anual da caldeira
  triggers:
    - trigger: time
      at: "09:00:00"
  conditions:
    - condition: template
      value_template: "{{ now().month == 9 and now().day == 1 }}"
  actions:
    - action: intellikeep.create_task
      data:
        name: Revisão anual da caldeira
        priority: high
        frequency: yearly
        due_date: "{{ (now() + timedelta(days=30)).isoformat() }}"
```

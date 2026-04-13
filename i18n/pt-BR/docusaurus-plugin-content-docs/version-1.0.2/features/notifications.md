---
sidebar_position: 4
title: Notificações e Sensores
---

# Notificações e Sensores

## Notificações

O IntelliKeep envia lembretes quando as tarefas estão se aproximando ou passando da data de vencimento.

### Como as notificações funcionam

- As verificações de notificação são executadas **a cada hora**
- Um lembrete é enviado **N dias antes** da data de vencimento da tarefa (configurável globalmente e por tarefa)
- Tarefas vencidas também disparam uma notificação
- A deduplicação de notificações é em memória e é reiniciada ao reiniciar o HA

### Canais de notificação

| Canal | Sempre ativo | Como configurar |
|---|---|---|
| Notificações persistentes do HA | Sim | Integrado, sem configuração necessária |
| Push mobile | Opcional | Defina um serviço `notify.*` em [Configuração](../configuration) |

### Gatilho de automação

O IntelliKeep dispara um evento que você pode usar em automações do HA:

```yaml
triggers:
  - trigger: event
    event_type: intellikeep_task_notification
    event_data:
      event_type: overdue   # ou "approaching"
```

Campos de dados do evento disponíveis: `task_id`, `title`, `message`, `event_type`.

## Entidades sensor

O IntelliKeep cria três entidades sensor que você pode usar em dashboards e automações:

| Entidade | Descrição |
|---|---|
| `sensor.intellikeep_tasks_due_today` | Número de tarefas com vencimento hoje |
| `sensor.intellikeep_tasks_overdue` | Número de tarefas atualmente vencidas |
| `sensor.intellikeep_next_due_task` | Nome e data de vencimento da próxima tarefa |

O estado dos sensores é atualizado:
- Imediatamente após qualquer ação de serviço que altere os dados das tarefas
- A cada 5 minutos via atualização agendada do coordenador

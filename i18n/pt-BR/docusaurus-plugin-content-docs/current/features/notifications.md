---
sidebar_position: 5
title: Notificações e Sensores
---

# Notificações e Sensores

## Notificações

O IntelliKeep avisa você quando as tarefas se aproximam do vencimento e de novo quando elas ficam atrasadas.

### Como as notificações funcionam

- As verificações rodam uma vez por hora
- Um lembrete é enviado quando a tarefa entra no prazo definido em **Avisar**: N dias antes do vencimento, configurado em cada tarefa (novas tarefas começam com o padrão das [opções da integração](../configuration))
- Uma tarefa atrasada recebe uma notificação própria, a menos que **Notificar quando atrasada** esteja desligado para ela
- Cada tarefa é notificada uma vez por etapa e data de vencimento. O que já foi enviado fica salvo, então reiniciar o Home Assistant não envia os mesmos lembretes de novo, e uma tarefa cuja data de vencimento muda recebe um lembrete para a nova data
- Concluir ou excluir uma tarefa limpa o estado de notificação dela
- As notificações saem no idioma do Home Assistant, definido em **Configurações → Sistema → Informações da casa** (**Geral** em versões anteriores): inglês, português ou espanhol, e inglês para qualquer outro idioma

### Canais de notificação

| Canal | Sempre ativo | Como configurar |
|---|---|---|
| Notificações persistentes do Home Assistant | Sim | Já vem embutido, não precisa configurar |
| Push no celular (ou qualquer serviço `notify.*`) | Opcional | Defina um serviço de notificação em [Configuração](../configuration#notification-service) |

### Evento de notificação {/* #notification-event */}

Toda notificação também dispara um evento `intellikeep_task_notification` que você pode usar em automações:

```yaml
triggers:
  - trigger: event
    event_type: intellikeep_task_notification
    event_data:
      event_type: overdue   # or "approaching"
```

| Campo | Descrição |
|---|---|
| `event_type` | `approaching` ou `overdue` |
| `task_id` | ID da tarefa |
| `title` | Título da notificação, no idioma do Home Assistant |
| `message` | Mensagem da notificação, no idioma do Home Assistant |
| `notification_id` | ID da notificação persistente |

### Evento de atualização de tarefa

O IntelliKeep também dispara `intellikeep_task_updated` sempre que uma tarefa muda, com os campos `task_id` e `action`. A ação é uma destas: `created`, `updated`, `completed`, `reopened`, `deleted`, `note_added` ou `note_deleted`.

```yaml
triggers:
  - trigger: event
    event_type: intellikeep_task_updated
    event_data:
      action: completed
```

Veja exemplos completos em [Automações](../automations).

## Entidades de sensor {/* #sensor-entities */}

O IntelliKeep cria três sensores que você pode usar em dashboards e automações:

| Entidade | Estado | Atributos |
|---|---|---|
| `sensor.intellikeep_tasks_due_today` | Quantidade de tarefas abertas que vencem hoje ou que já estão atrasadas | — |
| `sensor.intellikeep_tasks_overdue` | Quantidade de tarefas atrasadas | `overdue_tasks`: lista com `task_id`, `name`, `due_date` e `priority` de cada tarefa atrasada |
| `sensor.intellikeep_next_due_task` | Nome da tarefa aberta com o vencimento mais próximo | `task_id`, `due_date`, `priority`, `linked_entity_ids`, `frequency`, `repeat_interval`, `weekdays` |

Os IDs das entidades consideram o nome de instância padrão; veja [IDs das entidades](../configuration#entity-ids).

O IntelliKeep também tem uma [entidade de lista de tarefas e uma de calendário](./todo-and-calendar).

## Atualização dos dados

O estado das tarefas é atualizado:

- Logo depois de qualquer mudança feita pelo painel, pelo card, pela lista de tarefas ou por uma ação
- A cada 5 minutos, para que as contagens acompanhem o relógio (uma tarefa passa a vencer hoje ou fica atrasada à meia-noite local)
- O painel e o card recebem as atualizações assim que os dados mudam, sem recarregar a página

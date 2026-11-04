---
sidebar_position: 6
title: Serviços
---

# Serviços

O IntelliKeep oferece as ações do Home Assistant abaixo. Você pode chamá-las em automações, scripts ou em **Configurações → Ferramentas → Ações** (**Ferramentas de desenvolvedor → Ações** em versões anteriores do Home Assistant). O editor de ações mostra as ações, os campos e as opções no idioma do seu perfil (inglês, português ou espanhol).

Os IDs das tarefas aparecem nos atributos dos [sensores](./features/notifications#sensor-entities), nos [eventos](./features/notifications#notification-event) e nos diagnósticos.

## `intellikeep.create_task`

Cria uma nova tarefa.

```yaml
action: intellikeep.create_task
data:
  name: Replace HVAC filter
  icon: mdi:air-filter
  priority: high
  frequency: monthly
  repeat_interval: 3
  schedule_anchor: due_date
  due_date: "2026-12-01T09:00:00"
  linked_entity_ids:
    - area:living_room          # link to an area
    - device:abc123def456       # or a specific device ID
  notify_days_before: 3
  notify_on_overdue: true
```

| Campo | Obrigatório | Padrão | Descrição |
|---|---|---|---|
| `name` | Sim | — | Nome da tarefa |
| `description` | Não | — | Descrição em texto livre |
| `icon` | Não | `mdi:wrench-outline` | Ícone exibido ao lado da tarefa, por exemplo `mdi:air-filter` |
| `priority` | Não | `medium` | `low`, `medium`, `high` ou `critical` |
| `frequency` | Não | `one_time` | `one_time`, `daily`, `weekly`, `monthly` ou `yearly`. Em tarefas recorrentes, é a unidade de `repeat_interval` |
| `repeat_interval` | Não | `1` | Repete a cada N dias, semanas, meses ou anos (1–3650) |
| `schedule_anchor` | Não | `completion` | A partir de quando o próximo vencimento é contado: `completion` ou `due_date`. Veja [Tarefas recorrentes](./features/tasks#count-the-next-due-date-from) |
| `weekdays` | Não | — | Para tarefas semanais: os dias em que ela se repete, de `mon` a `sun`, por exemplo `[mon, wed, fri]` |
| `due_date` | Não | — | Data e hora em ISO 8601. Sem offset de UTC, é interpretada no fuso horário do Home Assistant. Meia-noite deixa a tarefa como dia inteiro |
| `linked_entity_ids` | Não | — | Áreas (`area:<area_id>`) e dispositivos (`device:<device_id>`) aos quais a tarefa será vinculada |
| `notify_days_before` | Não | Padrão da integração | Dias antes do vencimento para enviar um lembrete (0–365) |
| `notify_on_overdue` | Não | `true` | Envia uma notificação quando a tarefa fica atrasada |

### Exemplos

Uma tarefa semanal em dias específicos. A próxima ocorrência é sempre o próximo dia selecionado, no mesmo horário, então a agenda não se desloca quando uma tarefa é concluída com atraso:

```yaml
action: intellikeep.create_task
data:
  name: Take out the garbage
  icon: mdi:trash-can-outline
  frequency: weekly
  weekdays: [mon, wed, fri]
  due_date: "2026-11-09T07:00:00"
```

Uma tarefa a cada 10 dias, contados a partir de cada conclusão:

```yaml
action: intellikeep.create_task
data:
  name: Clean the coffee machine
  frequency: daily
  repeat_interval: 10
```

:::note Frequência `custom` legada
`frequency: custom` com `custom_days_interval`, das versões anteriores à 2.0, continua funcionando. Ela é salva como `frequency: daily` com esse `repeat_interval`.
:::

## `intellikeep.complete_task`

Marca uma tarefa como feita e registra uma conclusão. Em tarefas recorrentes, a próxima ocorrência é criada.

```yaml
action: intellikeep.complete_task
data:
  task_id: "<task_id>"
  completed_by: "Henrique"
  notes: "Replaced with a MERV-13 filter."
```

| Campo | Obrigatório | Descrição |
|---|---|---|
| `task_id` | Sim | ID da tarefa a concluir |
| `completed_by` | Não | Nome de quem concluiu a tarefa, exibido no histórico |
| `notes` | Não | Observações sobre a conclusão |

## `intellikeep.reopen_task`

Reabre uma tarefa concluída, deixando-a aberta de novo. A conclusão é desfeita: o registro dela sai do histórico e, em uma tarefa recorrente, a próxima ocorrência que ela criou é removida, a menos que essa ocorrência já tenha sido editada, recebido uma nota ou sido concluída.

```yaml
action: intellikeep.reopen_task
data:
  task_id: "<task_id>"
  performed_by: "Henrique"
```

| Campo | Obrigatório | Descrição |
|---|---|---|
| `task_id` | Sim | ID da tarefa a reabrir |
| `performed_by` | Não | Nome de quem reabriu a tarefa, mostrado no registro de atividades |

## `intellikeep.update_task`

Atualiza campos de uma tarefa existente. Só os campos enviados são alterados, e a mudança aparece no registro de atividades da tarefa.

```yaml
action: intellikeep.update_task
data:
  task_id: "<task_id>"
  priority: critical
  due_date: "2026-12-15T09:00:00"
  updated_by: "Henrique"
```

Aceita os mesmos campos de [`create_task`](#intellikeepcreate_task), além de:

| Campo | Obrigatório | Descrição |
|---|---|---|
| `task_id` | Sim | ID da tarefa a atualizar |
| `enabled` | Não | `false` fecha a tarefa sem registrar uma conclusão, `true` abre a tarefa de novo. Para concluir uma tarefa, use [`complete_task`](#intellikeepcomplete_task) |
| `updated_by` | Não | Nome de quem fez a alteração, exibido no registro de atividades |

## `intellikeep.delete_task`

Exclui uma tarefa de vez, junto com as notas e o histórico dela.

```yaml
action: intellikeep.delete_task
data:
  task_id: "<task_id>"
```

| Campo | Obrigatório | Descrição |
|---|---|---|
| `task_id` | Sim | ID da tarefa a excluir |

## `intellikeep.add_task_note`

Adiciona uma nota com data e hora a uma tarefa.

```yaml
action: intellikeep.add_task_note
data:
  task_id: "<task_id>"
  content: "Noticed some wear on the belt. Check again next month."
  added_by: "Henrique"
```

| Campo | Obrigatório | Descrição |
|---|---|---|
| `task_id` | Sim | ID da tarefa que vai receber a nota |
| `content` | Sim | Texto da nota |
| `added_by` | Não | Nome de quem adicionou a nota |

## `intellikeep.delete_task_note`

Exclui uma nota de uma tarefa.

```yaml
action: intellikeep.delete_task_note
data:
  task_id: "<task_id>"
  note_id: "<note_id>"
```

| Campo | Obrigatório | Descrição |
|---|---|---|
| `task_id` | Sim | ID da tarefa à qual a nota pertence |
| `note_id` | Sim | ID da nota a excluir |

## `intellikeep.load_sample_data`

Adiciona um conjunto de tarefas de manutenção de exemplo, com ícones. É útil para explorar o painel logo depois de uma instalação nova.

```yaml
action: intellikeep.load_sample_data
```

## `intellikeep.delete_all_data`

Exclui de vez todas as tarefas, notas e registros de conclusão. Só usuários administradores podem chamar esta ação.

```yaml
action: intellikeep.delete_all_data
```

:::danger
Esta ação não pode ser desfeita. Todos os dados das tarefas são removidos permanentemente.
:::

## Ações de lista de tarefas

A [lista de tarefas](./features/todo-and-calendar#to-do-list) também aceita as ações `todo.*` do Home Assistant, como `todo.add_item`, `todo.update_item` e `todo.remove_item`, em `todo.intellikeep_tasks`.

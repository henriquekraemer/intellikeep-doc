---
sidebar_position: 6
title: Serviços
---

# Serviços

O IntelliKeep expõe as seguintes ações de serviço do Home Assistant. Use-as em automações, scripts ou no painel de Ferramentas do Desenvolvedor → Ações.

## `intellikeep.create_task`

Cria uma nova tarefa.

```yaml
action: intellikeep.create_task
data:
  name: Trocar filtro do ar-condicionado
  priority: high
  frequency: monthly
  due_date: "2025-02-01T09:00:00"
  linked_entity_ids:
    - sensor.hvac_filter
  notify_days_before: 3
  notify_on_overdue: true
```

| Campo | Obrigatório | Padrão | Descrição |
|---|---|---|---|
| `name` | Sim | — | Nome da tarefa |
| `description` | Não | — | Descrição em texto livre |
| `priority` | Não | `medium` | `low`, `medium`, `high`, `critical` |
| `frequency` | Não | `one_time` | `one_time`, `daily`, `weekly`, `monthly`, `yearly`, `custom` |
| `custom_days_interval` | Não | — | Dias entre ocorrências quando `frequency` é `custom` |
| `due_date` | Não | — | String de data/hora ISO 8601 |
| `linked_entity_ids` | Não | — | Lista de IDs de entidades do HA para associar à tarefa |
| `notify_days_before` | Não | `1` | Dias antes do vencimento para enviar um lembrete |
| `notify_on_overdue` | Não | `true` | Enviar notificação quando a tarefa vencer |

## `intellikeep.complete_task`

Marca uma tarefa como concluída e registra uma entrada de execução. Para tarefas recorrentes, a próxima ocorrência é agendada automaticamente.

```yaml
action: intellikeep.complete_task
data:
  task_id: "<task_id>"
  completed_by: "Henrique"
  notes: "Substituído por um filtro MERV-13."
```

| Campo | Obrigatório | Descrição |
|---|---|---|
| `task_id` | Sim | ID da tarefa a concluir |
| `completed_by` | Não | Nome ou identificador de quem concluiu a tarefa |
| `notes` | Não | Notas opcionais de conclusão |

## `intellikeep.reopen_task`

Reabre uma tarefa concluída, marcando-a como pendente novamente.

```yaml
action: intellikeep.reopen_task
data:
  task_id: "<task_id>"
```

## `intellikeep.update_task`

Atualiza campos de uma tarefa existente. Apenas os campos fornecidos são alterados.

```yaml
action: intellikeep.update_task
data:
  task_id: "<task_id>"
  priority: critical
  due_date: "2025-03-01T09:00:00"
  updated_by: "Henrique"
```

Aceita os mesmos campos que `create_task`, mais:

| Campo | Obrigatório | Descrição |
|---|---|---|
| `task_id` | Sim | ID da tarefa a atualizar |
| `enabled` | Não | Ativar ou desativar a tarefa (`true` / `false`) |
| `updated_by` | Não | Nome ou identificador de quem fez a atualização |

## `intellikeep.delete_task`

Exclui permanentemente uma tarefa e seu histórico.

```yaml
action: intellikeep.delete_task
data:
  task_id: "<task_id>"
```

## `intellikeep.add_task_note`

Adiciona uma nota com timestamp a uma tarefa existente.

```yaml
action: intellikeep.add_task_note
data:
  task_id: "<task_id>"
  content: "Observado desgaste na correia — monitorar no próximo mês."
  added_by: "Henrique"
```

| Campo | Obrigatório | Descrição |
|---|---|---|
| `task_id` | Sim | ID da tarefa à qual adicionar a nota |
| `content` | Sim | Conteúdo em texto da nota |
| `added_by` | Não | Nome ou identificador de quem adicionou a nota |

## `intellikeep.delete_task_note`

Exclui uma nota específica de uma tarefa.

```yaml
action: intellikeep.delete_task_note
data:
  task_id: "<task_id>"
  note_id: "<note_id>"
```

| Campo | Obrigatório | Descrição |
|---|---|---|
| `task_id` | Sim | ID da tarefa que possui a nota |
| `note_id` | Sim | ID da nota a excluir |

## `intellikeep.delete_all_data`

Exclui permanentemente todas as tarefas, notas e histórico de execuções.

```yaml
action: intellikeep.delete_all_data
```

:::danger
Esta ação é irreversível. Todos os dados das tarefas serão removidos permanentemente.
:::

## `intellikeep.load_sample_data`

Preenche o IntelliKeep com tarefas de manutenção doméstica de exemplo. Útil para explorar a interface após uma instalação nova.

```yaml
action: intellikeep.load_sample_data
```

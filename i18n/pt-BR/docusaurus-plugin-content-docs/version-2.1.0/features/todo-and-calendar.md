---
sidebar_position: 4
title: Lista de Tarefas e Calendário
---

# Lista de Tarefas e Calendário

O IntelliKeep adiciona duas entidades que levam as suas tarefas para as **Listas de tarefas** e o **Calendário** do próprio Home Assistant. Assim, você pode ver e concluir as tarefas fora do painel do IntelliKeep, usá-las em outros cards e criar automações com elas.

## Lista de tarefas {/* #to-do-list */}

**`todo.intellikeep_tasks`** mostra as tarefas abertas, por data de vencimento, nas Listas de tarefas do Home Assistant, seguidas das tarefas concluídas nos últimos 30 dias.

- **Marcar** um item conclui a tarefa, e uma tarefa recorrente ganha a próxima ocorrência. **Desmarcar** reabre a tarefa e remove essa ocorrência, como o **Desfazer** do painel.
- O histórico da tarefa registra o usuário do Home Assistant que marcou ou desmarcou o item.
- Os itens **adicionados** à lista viram tarefas únicas. O nome, a descrição e a data de vencimento deles podem ser editados pela lista.
- **Excluir** um item aberto exclui a tarefa. As tarefas concluídas guardam o histórico, então não podem ser excluídas por aqui, e **Remover itens concluídos** é recusado. Elas saem da lista 30 dias depois da conclusão, ou você pode excluí-las no painel.
- As ações `todo.*` também funcionam, por exemplo `todo.add_item` a partir de um assistente de voz ou de uma automação:

```yaml
action: todo.add_item
target:
  entity_id: todo.intellikeep_tasks
data:
  item: Replace the doorbell battery
  due_date: "2026-12-01"
```

As tarefas criadas assim são tarefas únicas com a prioridade padrão. Abra-as no painel para definir uma prioridade, um ícone ou uma repetição.

## Calendário {/* #calendar */}

**`calendar.intellikeep_tasks`** mostra cada tarefa aberta na sua data de vencimento, incluindo as atrasadas. A entidade aparece no **Calendário** do Home Assistant e pode ser usada em cards de calendário.

- Uma tarefa com horário de vencimento é um evento naquele horário. Uma tarefa que vence à meia-noite (sem horário definido) é um evento de dia inteiro.
- As tarefas concluídas ficam de fora, para que uma tarefa feita antes da hora não dispare automações no horário de vencimento antigo.
- As repetições futuras não são projetadas: a próxima ocorrência só aparece quando a atual é concluída, então os gatilhos de calendário só disparam para tarefas reais. A [aba Calendário](./calendar#future-repeats) do painel mostra, sim, as repetições futuras.
- O calendário é somente leitura. Crie e edite tarefas no painel ou na lista de tarefas.

O estado da entidade fica `on` enquanto uma tarefa de dia inteiro vence hoje, e os atributos descrevem a tarefa que vence hoje ou a próxima a vencer.

### Gatilhos de calendário

Use um gatilho de calendário para agir quando uma tarefa vence:

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

As tarefas de dia inteiro começam à meia-noite local. O `offset` do gatilho desloca o horário de disparo para todas as tarefas; por exemplo, `offset: "-01:00:00"` dispara uma hora antes do vencimento de cada tarefa.

Há mais exemplos em [Automações](../automations).

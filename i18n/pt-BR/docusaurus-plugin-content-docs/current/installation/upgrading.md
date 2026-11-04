---
sidebar_position: 3
title: Atualizando da 1.x
---

# Atualizando da 1.x

O IntelliKeep 2.0 redesenhou o painel e o card de dashboard, e algumas coisas funcionam de um jeito diferente da 1.x. A maioria das instalações não precisa de nenhuma mudança, mas confira a lista abaixo antes de atualizar.

:::warning Faça um backup antes
Faça um backup do Home Assistant antes de atualizar. As tarefas salvas são convertidas na primeira inicialização da 2.x, e voltar para a 1.x depois disso não é suportado.
:::

## O que pode precisar da sua atenção

### O card de dashboard mostra menos tarefas

Agora o card lista **3 tarefas** por padrão, em vez de 10, e deixa as tarefas concluídas de fora. Para manter o comportamento antigo, adicione estas opções ao card:

```yaml
type: custom:intellikeep-card
max_tasks: 10
filter_status: [pending, due, overdue, completed]
```

Veja todas as opções em [Card Lovelace](../lovelace-card).

### Reabrir uma tarefa desfaz a conclusão

Agora `intellikeep.reopen_task` desfaz a conclusão: o registro dela sai do histórico, e a próxima ocorrência que essa conclusão criou para uma tarefa recorrente é removida, a menos que alguém já tenha editado essa ocorrência, adicionado uma nota a ela ou concluído. Na 1.x, reabrir uma tarefa recorrente deixava duas ocorrências abertas.

Confira as automações que reabrem tarefas.

### `frequency: custom` é salvo como `daily`

A antiga frequência **custom**, com `custom_days_interval`, agora é uma tarefa diária com um [`repeat_interval`](../features/tasks#recurring-tasks). As tarefas existentes são convertidas quando o IntelliKeep carrega, e as ações que ainda enviam `frequency: custom` continuam funcionando.

Porém, o sensor `next_due_task` e o painel agora informam `daily`, então templates que comparam a frequência com `custom` precisam ser atualizados.

### A 1.x ignora os novos campos das tarefas

Se mesmo assim você voltar para a 1.x, os campos adicionados na 2.0 são ignorados: uma tarefa que se repete a cada 3 dias passaria a se repetir todo dia, e uma tarefa contada a partir do vencimento voltaria a ser contada a partir da conclusão.

## Novidades da 2.0

- Um painel redesenhado: tarefas agrupadas por vencimento, prioridade ou área, uma caixa de seleção com Desfazer e um menu ⋮ com Editar, Duplicar, Histórico e Excluir
- Tarefas que se repetem a cada N dias, semanas, meses ou anos, contados a partir da conclusão ou da data de vencimento
- Um ícone por tarefa
- Uma entidade de lista de tarefas e uma entidade de calendário para as Listas de tarefas e o Calendário do próprio Home Assistant
- Repetições futuras das tarefas recorrentes na aba Calendário do painel
- Uma nova aba Histórico, com quem concluiu cada tarefa e se ela foi feita no prazo
- Um card de dashboard redesenhado, com uma caixa de seleção por tarefa

A lista completa está no [changelog](https://github.com/henriquekraemer/intellikeep/blob/main/CHANGELOG.md).

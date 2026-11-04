---
sidebar_position: 1
title: Tarefas
---

# Tarefas

A aba **Tarefas** é a tela principal do painel do IntelliKeep. Ela lista as suas tarefas, permite concluí-las com um clique e abre a janela da tarefa para criar ou editar.

<img
  src={require('@site/static/img/screenshots/tasks-desktop.png').default}
  alt="Tarefas abertas agrupadas em Atrasadas, Hoje, Esta semana e Mais tarde, cada uma com caixa de seleção, ícone, prioridade e data de vencimento"
  className="ik-screenshot"
/>

## A lista de tarefas

No topo da lista, você escolhe entre:

- **Abertas**: todas as tarefas que ainda precisam ser feitas
- **Concluídas**: as tarefas concluídas nos últimos 30 dias, das mais recentes para as mais antigas (as anteriores continuam na aba [Histórico](./history))

Por padrão, as tarefas abertas são agrupadas por vencimento: **Atrasadas**, **Hoje**, **Esta semana**, **Mais tarde** e **Sem data prevista**. Em **Agrupar por**, você troca o agrupamento para **Prioridade** ou **Área**, ou desliga o agrupamento (**Nenhum**). A escolha fica salva no navegador.

Cada linha mostra o ícone da tarefa, o nome e o número (`#001`), a descrição, a prioridade e uma etiqueta de vencimento, como *3 dias de atraso*, *Hoje, 19:00* ou *sáb., 7 de nov.* O vermelho e o âmbar ficam reservados para o que precisa de atenção: tarefas atrasadas, tarefas que vencem hoje e a prioridade **Crítica**.

### Concluindo uma tarefa

Marque a caixa de seleção de uma tarefa para concluí-la. Aparece a mensagem *Tarefa concluída* com **Desfazer**, que reabre a tarefa na mesma hora. Concluir uma tarefa recorrente cria a próxima ocorrência (veja [Tarefas recorrentes](#recurring-tasks)).

O nome do usuário do Home Assistant que concluiu a tarefa fica registrado no histórico dela.

### O menu ⋮

Cada tarefa tem um menu ⋮ com:

- **Editar**: abre a janela da tarefa
- **Duplicar**: abre o formulário de nova tarefa com os mesmos campos já preenchidos
- **Histórico**: abre a janela da tarefa na aba Histórico
- **Excluir**: exclui a tarefa, depois de uma confirmação

### Busca e filtros {/* #search-and-filters */}

- A busca (**Buscar tarefas**) encontra tarefas pelo nome, pela descrição ou pelo número
- **Filtros** restringe a lista por **prioridade**, **área** e **dispositivo**. Quando você filtra por área e por dispositivo ao mesmo tempo, pode combinar os dois como *Área OU dispositivo* ou *Área E dispositivo*

Ao escolher uma área, o seletor de dispositivos passa a mostrar só os dispositivos daquela área. Os filtros ativos aparecem como chips, que você pode remover um a um ou todos de uma vez, e ficam salvos no navegador.

### No celular

No celular e em janelas estreitas (com menos de 600px de largura, ou quando o Home Assistant esconde a barra lateral), o painel se adapta:

- As abas Tarefas, Calendário e Histórico ocupam toda a largura, e a busca vira uma lupa no cabeçalho
- Cada linha mantém só a caixa de seleção e o nome, com o vencimento, a prioridade e a repetição em uma linha abaixo
- **Agrupar por** vai para dentro de **Filtros**, e **Adicionar tarefa** vira um botão flutuante

<img
  src={require('@site/static/img/screenshots/tasks-mobile.png').default}
  alt="Lista de tarefas no celular"
  className="ik-screenshot ik-screenshot--phone"
/>

## Criando e editando uma tarefa

Clique em **Adicionar tarefa** na barra de ferramentas da lista para criar uma tarefa. Para abrir uma tarefa, clique nela ou escolha **Editar** no menu ⋮ dela. Também é possível criar tarefas com a ação [`intellikeep.create_task`](../services#intellikeepcreate_task) ou pela [lista de tarefas](./todo-and-calendar#to-do-list) do Home Assistant.

<img
  src={require('@site/static/img/screenshots/dialog-desktop.png').default}
  alt="Janela da tarefa com nome, ícone, prioridade, data e hora de vencimento e a frequência com que a tarefa se repete"
  className="ik-screenshot"
/>

O cabeçalho da janela mostra o nome da tarefa, o número dela e como ela se repete, além de um menu ⋮ com **Duplicar** e **Excluir**. Uma tarefa existente tem três abas: **Detalhes**, **Notas** e **Histórico**. No rodapé ficam **Concluir**, **Cancelar** e **Salvar**.

### Campos da tarefa

| Campo | Descrição |
|---|---|
| **Nome** | Título da tarefa (obrigatório) |
| **Ícone** | Qualquer ícone do Material Design Icons, escolhido no seletor de ícones do Home Assistant (busque por nome ou palavra-chave). Tarefas sem ícone mostram uma chave inglesa (`mdi:wrench-outline`) |
| **Descrição** | Texto livre opcional |
| **Prioridade** | **Baixa**, **Média**, **Alta** ou **Crítica** |
| **Data prevista** e **Hora** | Quando a tarefa vence (em tarefas recorrentes, a data aparece como **Próximo vencimento**). O **×** ao lado da hora remove o horário e deixa a tarefa como *dia inteiro* |
| **Repetição** | *Não repete*, ou *Repetir a cada N dias, semanas, meses ou anos* |
| **Repetir em** | Para tarefas semanais: os dias da semana em que ela se repete |
| **Contar o próximo vencimento a partir da** | Para tarefas recorrentes: **Data de conclusão** ou **Data de vencimento original** (veja abaixo) |
| **Vinculada a** | Áreas e dispositivos do Home Assistant, exibidos como chips removíveis. Os filtros de área e dispositivo usam esses vínculos |
| **Avisar** | Quantos dias antes do vencimento o lembrete é enviado. Novas tarefas começam com o [padrão das opções da integração](../configuration) |
| **Notificar quando atrasada** | Envia uma notificação assim que a tarefa fica atrasada |

### Tarefas de dia inteiro

Uma data de vencimento sem horário é uma tarefa de dia inteiro. Ela é salva como meia-noite, assim como as datas definidas pelo calendário e pelas Listas de tarefas do Home Assistant. Quando vence hoje, essa tarefa mostra **Hoje** em vez de *Hoje, 00:00*, e a janela da tarefa mostra o horário como **Dia inteiro**.

## Tarefas recorrentes {/* #recurring-tasks */}

Quando você conclui uma tarefa recorrente, o IntelliKeep registra a conclusão e cria a próxima ocorrência, com um novo número de tarefa e o mesmo nome, ícone, prioridade, vínculos e configurações de notificação. Cada ocorrência guarda as próprias notas e o próprio histórico, e a aba Histórico da janela da tarefa lista as ocorrências anteriores.

### Repetir a cada N períodos

Uma tarefa se repete a cada N **dias**, **semanas**, **meses** ou **anos**. Por exemplo, *Repetir a cada 3 meses* para o filtro do ar-condicionado, ou *Repetir a cada 2 semanas* para limpar a geladeira.

Repetições mensais e anuais mantêm o dia do mês e, nos meses mais curtos, caem no último dia: uma tarefa que vence em 31 de janeiro e se repete todo mês passa a vencer em 28 (ou 29) de fevereiro.

### A partir de quando contar o próximo vencimento {/* #count-the-next-due-date-from */}

A opção **Contar o próximo vencimento a partir da** define a partir de quando a próxima data de vencimento é contada:

- **Data de conclusão** (o padrão): conta a partir do momento em que a tarefa é feita. Se você conclui uma tarefa mensal com 5 dias de atraso, a próxima também fica 5 dias mais tarde. Bom para coisas que se desgastam com o tempo, como um filtro.
- **Data de vencimento original**: conta a partir da própria data de vencimento da tarefa, mantendo um calendário fixo. Os períodos que já passaram são pulados, então uma conclusão atrasada nunca cria uma tarefa que já nasce atrasada. Bom para coisas ligadas ao calendário, como uma inspeção anual em março.

### Dias específicos da semana

Uma tarefa semanal pode se repetir em dias escolhidos, por exemplo a coleta de lixo às segundas, quartas e sextas (**Seg**, **Qua** e **Sex**). A próxima ocorrência é o próximo dia selecionado, no horário original da tarefa, então a agenda não se desloca quando uma tarefa é concluída com atraso. Com *Repetir a cada 2 semanas*, a tarefa se repete nos dias selecionados uma semana sim, outra não.

Se nenhum dia for selecionado, uma tarefa semanal se repete a cada 7 dias (ou a cada N semanas) a partir da última conclusão.

:::note
Nas versões anteriores à 2.0, os intervalos em dias usavam a frequência **custom**. Essas tarefas agora são tarefas diárias com um intervalo de repetição e funcionam do mesmo jeito. Veja [Atualizando da 1.x](../installation/upgrading).
:::

## Status da tarefa

| Status | Significado |
|---|---|
| `pending` | Aberta, vence mais tarde (ou não tem data de vencimento) |
| `due` | Aberta e vence hoje |
| `overdue` | Aberta, e a data de vencimento já passou. As tarefas ficam atrasadas no dia seguinte ao vencimento, à meia-noite local |
| `completed` | Feita. Tarefas concluídas ficam somente leitura até você reabri-las |

O status é calculado a partir da data de vencimento, no fuso horário do Home Assistant, e nunca é salvo.

## Notas

A aba **Notas** da janela da tarefa guarda anotações sobre a tarefa. Cada nota tem data e hora e registra o usuário do Home Assistant que a adicionou. Você pode adicionar e excluir notas ali, ou com as ações [`intellikeep.add_task_note`](../services#intellikeepadd_task_note) e [`intellikeep.delete_task_note`](../services#intellikeepdelete_task_note).

## Histórico e registro de atividades da tarefa

A aba **Histórico** da janela da tarefa mostra:

- Cada conclusão da tarefa, com quem concluiu, quando e se foi com atraso
- As ocorrências anteriores de uma tarefa recorrente (**Ocorrências Anteriores**)
- O **Registro de Atividades**: cada edição (com os campos alterados), conclusão, reabertura e nota adicionada ou excluída

## Reabrindo uma tarefa {/* #reopening-a-task */}

Abra uma tarefa concluída e clique em **Reabrir**, use **Desfazer** logo depois de concluí-la ou desmarque-a na [lista de tarefas](./todo-and-calendar#to-do-list). Reabrir desfaz a conclusão: o registro dela sai do histórico, e a próxima ocorrência que ela criou para uma tarefa recorrente é removida, a menos que alguém já tenha editado essa ocorrência, adicionado uma nota a ela ou concluído.

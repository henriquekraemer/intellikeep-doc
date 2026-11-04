---
sidebar_position: 2
title: Calendário
---

# Calendário

A aba **Calendário** organiza as suas tarefas por data de vencimento, em um layout que segue o calendário do próprio Home Assistant.

<img
  src={require('@site/static/img/screenshots/calendar-desktop.png').default}
  alt="Visualização por mês com tarefas concluídas, tarefas abertas e as repetições futuras das tarefas recorrentes com contorno tracejado"
  className="ik-screenshot"
/>

## Visualizações e navegação

- **Mês** e **Semana** alternam entre as duas visualizações
- **Hoje**, **Anterior** e **Próximo** navegam entre meses ou semanas, e a barra de ferramentas mostra o período que você está vendo
- A aba sempre abre no mês atual

Os dias e as semanas seguem o fuso horário e o primeiro dia da semana definidos no seu perfil de usuário do Home Assistant.

## Como as tarefas aparecem

- Tarefas com horário mostram a hora ao lado de um ponto; tarefas de dia inteiro aparecem como uma barra colorida
- A cor marca só o que precisa de atenção: tarefas atrasadas e tarefas que vencem hoje
- Tarefas com prioridade **Crítica** mostram o ícone da prioridade
- Tarefas concluídas aparecem em cinza, com um check
- Um dia com mais tarefas do que cabem mostra **+N outras**, que abre aquela semana

Clique em uma tarefa para abri-la na janela da tarefa. Clique no espaço vazio de um dia para adicionar uma tarefa que vence naquele dia.

## Repetições futuras {/* #future-repeats */}

As tarefas recorrentes também mostram as suas **repetições futuras**, as ocorrências depois da que está aberta, com contorno tracejado e um ícone de repetição. Clique em uma delas para abrir a tarefa.

Elas são projetadas do mesmo jeito que a conclusão cria a próxima ocorrência, supondo que cada uma seja feita na data de vencimento (e uma atrasada, hoje). Por isso, são exatas para tarefas contadas a partir do vencimento e uma estimativa para tarefas contadas a partir da conclusão, cujas datas reais dependem de quando cada ocorrência for feita.

Para esconder as repetições futuras, desligue o interruptor **Mostrar repetições futuras** em **Filtros**.

:::note
As repetições futuras aparecem só no painel. A entidade [`calendar.intellikeep_tasks`](./todo-and-calendar#calendar) lista apenas as ocorrências abertas, então os gatilhos de calendário só disparam para tarefas reais.
:::

## Filtros

**Filtros** tem os mesmos filtros de área, dispositivo e prioridade da aba [Tarefas](./tasks#search-and-filters), além do interruptor das repetições futuras.

## No celular

No celular, o mês vira uma grade pequena com um ponto por tarefa, e as tarefas do dia escolhido aparecem listadas abaixo dela. A visualização por semana é uma lista de dias.

<img
  src={require('@site/static/img/screenshots/calendar-mobile.png').default}
  alt="Calendário do mês no celular, com as tarefas do dia escolhido abaixo dele"
  className="ik-screenshot ik-screenshot--phone"
/>

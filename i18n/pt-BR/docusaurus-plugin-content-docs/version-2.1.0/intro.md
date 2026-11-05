---
sidebar_position: 1
slug: /
title: Introdução
---

# IntelliKeep

O IntelliKeep é uma integração personalizada, gratuita e de código aberto para o Home Assistant que organiza as tarefas de manutenção da sua casa. Ele reúne tudo em um só lugar, da troca mensal de um filtro à revisão anual do aquecedor, e avisa você antes que as coisas vençam. Cada tarefa guarda o próprio histórico, então você sempre sabe o que foi feito, por quem e quando.

<img
  src={require('@site/static/img/screenshots/tasks-desktop.png').default}
  alt="Painel do IntelliKeep com as tarefas abertas agrupadas em Atrasadas, Hoje, Esta semana e Mais tarde"
  className="ik-screenshot"
/>

## O que o IntelliKeep faz

- Tarefas únicas e recorrentes, que se repetem a cada N dias, semanas, meses ou anos, contados a partir da conclusão ou da data de vencimento
- Tarefas semanais fixadas em dias específicos da semana, como a coleta de lixo às segundas, quartas e sextas
- Quatro níveis de prioridade (baixa, média, alta e crítica), exibidos com um ícone e um rótulo
- Um ícone por tarefa, escolhido entre os Material Design Icons
- Vínculos com áreas do Home Assistant ou com dispositivos específicos
- Notas com data e hora em cada tarefa, com o nome de quem as escreveu
- Um registro de atividades por tarefa, com edições, conclusões, reaberturas e alterações nas notas
- Um calendário com visualização por mês e por semana, as repetições futuras das tarefas recorrentes e filtros por área, dispositivo e prioridade
- Um histórico de conclusões que mostra quem fez cada tarefa e se ela foi feita no prazo, com exportação em CSV e impressão
- Lembretes pelas notificações persistentes do Home Assistant, com push opcional no celular
- Três sensores: `tasks_due_today`, `tasks_overdue` e `next_due_task`
- Uma lista de tarefas (`todo.intellikeep_tasks`) para as Listas de tarefas do Home Assistant e um calendário (`calendar.intellikeep_tasks`) para o Calendário, os cards de calendário e os gatilhos de calendário
- Um card de dashboard que lista as tarefas mais urgentes e as conclui com um clique
- Um painel responsivo que segue a interface do Home Assistant no computador e no celular, em inglês, português e espanhol

## O que o IntelliKeep não faz

- Descoberta automática de dispositivos
- Atualizações de firmware de fabricantes
- Autenticação em contas externas ou sincronização com plataformas de tarefas de terceiros

## Início rápido

1. [Instale via HACS ou Marketplace](./installation/hacs) (recomendado)
2. Reinicie o Home Assistant
3. Adicione a integração em **Configurações → Dispositivos & serviços**
4. Abra o painel do IntelliKeep na barra lateral e crie sua primeira tarefa

:::tip Vindo da 1.x?
A versão 2.0 redesenhou o painel e o card de dashboard e mudou alguns padrões. Leia [Atualizando da 1.x](./installation/upgrading) antes de atualizar.
:::

---
sidebar_position: 8
title: Solução de Problemas
---

# Solução de Problemas

## O painel ou o card não mostra os dados atuais

1. Vá em **Configurações → Dispositivos & serviços** e confirme que a entrada do IntelliKeep está carregada e sem erros
2. Baixe os diagnósticos da entrada (**Download de diagnósticos**) e confira se os contadores de tarefas fazem sentido
3. Se você acabou de atualizar o IntelliKeep, **reinicie o Home Assistant** e recarregue a página do navegador (limpe o cache, se precisar) para carregar os novos arquivos do frontend

## "Custom element doesn't exist: intellikeep-card"

O dashboard não encontra o código do card.

1. Se os seus dashboards são configurados em YAML, adicione o recurso do card manualmente, como descrito em [Dashboards em modo YAML](./lovelace-card#yaml-mode-dashboards)
2. Caso contrário, confira em **Configurações → Dashboards → ⋮ → Recursos** se `/intellikeep_static/intellikeep-card.js` aparece na lista, reinicie o Home Assistant e recarregue a página

## As notificações no celular não chegam

1. Em **Configurações → Ferramentas → Ações** (**Ferramentas de desenvolvedor → Ações** em versões anteriores do Home Assistant), confira se o serviço `notify.*` que você configurou existe mesmo
2. Deixe o campo **Serviço de Notificação** vazio para voltar a usar só as notificações persistentes
3. Procure erros do IntelliKeep nos **logs do Home Assistant** (filtre por `intellikeep`)
4. Lembre que cada tarefa é notificada uma vez por etapa, até o Home Assistant reiniciar

## Tarefas aparecem atrasadas sem motivo

1. Confira o **fuso horário** do Home Assistant em **Configurações → Sistema → Informações da casa** (**Geral** em versões anteriores). As tarefas vencem e ficam atrasadas à meia-noite nesse fuso
2. Confira o fuso horário do seu **perfil de usuário**: as datas no painel seguem esse fuso
3. Confirme o valor de `due_date` salvo nos diagnósticos da tarefa
4. Abra a aba **Histórico** da tarefa para ver se ela foi concluída e depois reaberta

## Uma tarefa recorrente ganhou uma próxima data inesperada

1. Confira a opção **Contar o próximo vencimento a partir da** na janela da tarefa. Com **Data de conclusão**, uma conclusão atrasada também empurra a próxima ocorrência; com **Data de vencimento original**, a tarefa mantém um calendário fixo
2. Em tarefas semanais com dias selecionados, a próxima ocorrência é o próximo dia selecionado depois do vencimento atual, no horário original da tarefa
3. Na aba Calendário do painel, as datas das repetições futuras são uma estimativa para tarefas contadas a partir da conclusão

## A integração não carrega depois de uma atualização

1. Procure nos logs erros de Python relacionados a `custom_components.intellikeep`
2. Confirme que a pasta `custom_components/intellikeep/` inteira foi substituída, e não só alguns arquivos
3. Se você usa o HACS, baixe a integração de novo e reinicie
4. Confira se o Home Assistant está na versão 2026.1 ou mais recente

## Limitações conhecidas

- O IntelliKeep é de instância única: só uma entrada da integração é permitida por instalação do Home Assistant
- Os dados das tarefas ficam salvos localmente (em `.storage/intellikeep`) e não são compartilhados entre instalações do Home Assistant
- As tarefas não são entidades individuais: os sensores as resumem, e a lista de tarefas e o calendário as listam
- A entidade `calendar.intellikeep_tasks` mostra só a ocorrência atual de cada tarefa recorrente. A aba Calendário do painel projeta as próximas e, para tarefas contadas a partir da conclusão, essas datas são uma estimativa
- O controle de notificações duplicadas fica em memória e é zerado quando o Home Assistant reinicia

## Removendo o IntelliKeep

1. Vá em **Configurações → Dispositivos & serviços**
2. Abra o **IntelliKeep** e escolha **Excluir**
3. Remova os cards de dashboard e as automações que ainda usam ações, entidades ou eventos do IntelliKeep
4. Se você instalou manualmente, apague `custom_components/intellikeep/` da pasta de configuração do Home Assistant

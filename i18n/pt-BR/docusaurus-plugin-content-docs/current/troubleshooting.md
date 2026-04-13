---
sidebar_position: 8
title: Solução de Problemas
---

# Solução de Problemas

## Painel ou cartão não exibe dados atuais

1. Vá em **Configurações → Dispositivos e Serviços** e confirme que a entrada IntelliKeep está carregada e não exibe erros
2. Baixe o **Diagnóstico** da entrada de configuração e verifique se os contadores de tarefas correspondem ao esperado
3. Se você reconstruiu ou atualizou o frontend recentemente, **reinicie o Home Assistant** para recarregar os assets estáticos

## Notificações mobile não chegam

1. Em **Ferramentas do Desenvolvedor → Ações**, verifique se o serviço `notify.*` que você configurou realmente existe
2. Deixe o campo **Serviço de Notificação** vazio para usar apenas as notificações persistentes do HA
3. Verifique os **logs do Home Assistant** para erros relacionados ao IntelliKeep (filtre por `intellikeep`)

## Tarefas aparecem vencidas inesperadamente

1. Verifique o **horário do sistema e fuso horário** do Home Assistant — o IntelliKeep usa o horário do sistema do HA
2. Confirme o valor de `due_date` armazenado no diagnóstico da tarefa
3. Abra o **Log de Atividade** da tarefa para ver se ela foi concluída e reaberta

## Integração falha ao carregar após atualização

1. Limpe o cache do navegador e recarregue
2. Verifique os logs para erros de importação Python relacionados a `custom_components.intellikeep`
3. Certifique-se de que todo o diretório `custom_components/intellikeep/` foi substituído (não apenas alguns arquivos)
4. Se estiver usando o HACS, baixe novamente a integração e reinicie

## Limitações conhecidas

- O IntelliKeep é **instância única** — apenas uma entrada de integração por instância do Home Assistant
- Os dados das tarefas são armazenados localmente e não são compartilhados entre instâncias do HA
- A deduplicação de notificações é em memória e **reinicia após um restart do HA**
- Os sensores resumem o estado das tarefas; entidades de tarefa individuais não são criadas

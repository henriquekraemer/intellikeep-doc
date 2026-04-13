---
sidebar_position: 3
title: Configuração
---

# Configuração

## Configuração inicial

Durante o assistente de configuração da integração você pode definir:

| Opção | Padrão | Descrição |
|---|---|---|
| **Nome da Instância** | `IntelliKeep` | Rótulo exibido no Home Assistant |
| **Notificar N dias antes** | `1` | Dias antes do vencimento da tarefa para enviar um lembrete |
| **Serviço de Notificação** | *(vazio)* | Serviço `notify.*` opcional, ex.: `notify.mobile_app_meu_celular` |

## Alterando as configurações depois

Todas as opções podem ser atualizadas após a instalação:

1. Vá em **Configurações → Dispositivos e Serviços**
2. Encontre a entrada **IntelliKeep**
3. Clique em **Configurar** para ajustar as configurações, ou **Reconfigurar** para executar o assistente novamente

## Serviço de notificação

Deixe o campo **Serviço de Notificação** vazio para usar apenas as notificações persistentes do Home Assistant (ícone de sino na interface do HA).

Para receber também notificações push no celular, insira um nome de serviço `notify.*`. Você pode encontrar os serviços disponíveis em **Ferramentas do Desenvolvedor → Ações**.

Exemplos:
- `notify.mobile_app_meu_celular`
- `notify.all_devices`

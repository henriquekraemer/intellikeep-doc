---
sidebar_position: 3
title: Configuração
---

# Configuração

## Configuração inicial

No assistente de configuração da integração, você pode definir:

| Opção | Padrão | Descrição |
|---|---|---|
| **Nome da Instância** | `IntelliKeep` | Nome do dispositivo IntelliKeep no Home Assistant. Os IDs das entidades são criados a partir dele |
| **Antecedência Padrão para Notificações (dias)** | `1` | Quantos dias antes do vencimento o lembrete é enviado (0–30). Novas tarefas começam com esse valor, e cada tarefa pode alterá-lo |
| **Serviço de Notificação** | *(vazio)* | Serviço `notify.*` opcional, por exemplo `notify.mobile_app_my_phone` |

Só é possível configurar uma instância do IntelliKeep por instalação do Home Assistant.

## Alterando as configurações depois

Todas as opções podem ser alteradas depois da instalação:

1. Vá em **Configurações → Dispositivos & serviços**
2. Encontre a entrada do **IntelliKeep**
3. Clique em **Configurar** para ajustar as opções, ou escolha **Reconfigurar** no menu ⋮ para rodar o assistente de configuração de novo

O IntelliKeep recarrega uma vez com as novas configurações.

## Serviço de notificação {/* #notification-service */}

Deixe o **Serviço de Notificação** vazio se você quiser apenas as notificações persistentes do Home Assistant (o ícone de sino na interface).

Para receber também notificações push no celular, informe o nome de um serviço `notify.*`. Os serviços disponíveis na sua instalação aparecem em **Configurações → Ferramentas → Ações** (**Ferramentas de desenvolvedor → Ações** em versões anteriores do Home Assistant).

Exemplos de valores:
- `notify.mobile_app_my_phone`
- `notify.all_devices`

Veja em [Notificações e Sensores](./features/notifications) quando os lembretes são enviados.

## IDs das entidades {/* #entity-ids */}

O IntelliKeep cria um dispositivo, com o nome definido em **Nome da Instância**, com estas entidades:

| Entidade | Descrição |
|---|---|
| `sensor.intellikeep_tasks_due_today` | Tarefas que vencem hoje ou que já estão atrasadas |
| `sensor.intellikeep_tasks_overdue` | Tarefas atrasadas |
| `sensor.intellikeep_next_due_task` | A próxima tarefa a vencer |
| `todo.intellikeep_tasks` | [Lista de tarefas](./features/todo-and-calendar#to-do-list) com as tarefas abertas e as concluídas recentemente |
| `calendar.intellikeep_tasks` | [Calendário](./features/todo-and-calendar#calendar) com as tarefas abertas nas suas datas de vencimento |

Esses IDs consideram o nome de instância padrão. Com outro nome, a parte `intellikeep` acompanha o nome escolhido (por exemplo, `todo.home_tasks` para uma instância chamada *Home*).

## Idioma, datas e horários

O painel e o card de dashboard seguem o idioma definido no seu perfil de usuário do Home Assistant (estão disponíveis inglês, português e espanhol, com o inglês como alternativa). Datas e horários seguem o idioma, o fuso horário, o primeiro dia da semana e o formato de 12/24 horas do perfil.

As tarefas vencem e ficam atrasadas à meia-noite local, no fuso horário do Home Assistant.

## Configurações do painel

O ícone de engrenagem no cabeçalho do painel abre as configurações do próprio painel:

- **Animações de tarefas**: desliga as transições ao concluir, excluir, reabrir ou navegar entre tarefas. Essa escolha fica salva por navegador.
- **Excluir todos os dados**: exclui de vez todas as tarefas, notas e registros de conclusão. Pede confirmação, e só usuários administradores veem esse botão.

Abaixo das configurações, o painel lista as ações, os eventos e os IDs de entidade do IntelliKeep na sua instalação, e o arquivo onde os dados ficam salvos.

---
sidebar_position: 1
slug: /
title: Introdução
---

# IntelliKeep

**IntelliKeep** é um sistema de gerenciamento de tarefas de manutenção doméstica, criado como uma integração personalizada gratuita e de código aberto para o Home Assistant. Ele centraliza todas as tarefas da casa — de simples trocas de filtro a verificações periódicas — oferecendo alertas automáticos e um histórico completo das tarefas.

## O que o IntelliKeep faz

- Criar **tarefas únicas ou recorrentes** (diária, semanal, mensal, anual ou intervalo personalizado)
- Definir **níveis de prioridade** (baixo, médio, alto, crítico) com indicadores visuais coloridos
- Vincular tarefas a **áreas do Home Assistant ou dispositivos específicos**
- Adicionar **notas com timestamp** e registro de autor por tarefa
- Registrar um **log de atividade** completo para cada edição, conclusão e reabertura
- Visualizar tarefas em um **Calendário** (semana/mês) com filtros por área, dispositivo e prioridade
- Consultar um **Histórico de Execuções** completo com exportação CSV e suporte a impressão
- Receber **notificações** via notificações persistentes do HA ou push mobile opcional
- Monitorar o estado das tarefas via três **entidades sensor**: `tasks_due_today`, `tasks_overdue`, `next_due_task`
- Exibir tarefas vencidas e em aberto no dashboard do HA usando o **cartão Lovelace**

## O que o IntelliKeep não faz

- Descoberta automática de dispositivos
- Atualizações de firmware de fabricantes
- Autenticação de conta externa ou sincronização com plataformas de tarefas de terceiros

## Início rápido

1. [Instalar via HACS](./installation/hacs) (recomendado)
2. Reiniciar o Home Assistant
3. Adicionar a integração em **Configurações → Dispositivos e Serviços**
4. Abrir o **painel IntelliKeep** na barra lateral do HA e criar sua primeira tarefa

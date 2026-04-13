---
sidebar_position: 1
title: Tarefas
---

# Tarefas

A visualização de Tarefas é o painel principal do IntelliKeep. Exibe todas as tarefas pendentes e concluídas com filtros e busca avançados.

## Criando uma tarefa

As tarefas podem ser criadas pela interface do painel ou via a ação de serviço [`intellikeep.create_task`](../services#intellikeepcreate_task).

### Campos da tarefa

| Campo | Descrição |
|---|---|
| **Nome** | Título da tarefa |
| **Prioridade** | `baixa`, `média`, `alta` ou `crítica` |
| **Data de vencimento** | Quando a tarefa vence |
| **Frequência** | Recorrência: `one_time`, `daily`, `weekly`, `monthly`, `yearly` ou `custom` (com `custom_days_interval`) |
| **Entidades vinculadas** | Áreas do HA ou IDs de dispositivos específicos |
| **Notificar N dias antes** | Sobrescreve o prazo global de notificação para esta tarefa |
| **Descrição** | Descrição em texto livre (opcional) |

## Tarefas recorrentes

Quando uma tarefa recorrente é concluída, uma nova instância é criada automaticamente com a próxima data de vencimento calculada a partir da configuração de frequência.

Frequências suportadas:
- `one_time` — sem recorrência
- `daily`
- `weekly`
- `monthly`
- `yearly`
- `custom` — especifique o número de dias via `custom_days_interval`

## Níveis de prioridade

As prioridades são exibidas como uma barra colorida em cada cartão de tarefa:

| Prioridade | Cor |
|---|---|
| Baixa | Verde |
| Média | Amarelo |
| Alta | Laranja |
| Crítica | Vermelho |

## Filtros e busca

A visualização de Tarefas suporta filtros por:
- **Área** — exibir tarefas vinculadas a uma área específica do HA
- **Dispositivo** — exibir tarefas vinculadas a um dispositivo específico
- **Prioridade** — filtrar por um ou mais níveis de prioridade
- **Busca por texto** — filtrar pelo nome da tarefa

## Notas

Cada tarefa possui uma seção de Notas dedicada. As notas têm timestamp e registram o autor (usuário do HA que as adicionou). As notas podem ser adicionadas, visualizadas e excluídas na visualização de detalhes da tarefa.

## Log de atividade

Cada alteração em uma tarefa é registrada no seu Log de Atividade:
- Campos editados
- Tarefa concluída (com timestamp de conclusão)
- Tarefa reaberta
- Notas adicionadas ou excluídas

---
sidebar_position: 5
title: Cartão Lovelace
---

# Cartão Lovelace

O IntelliKeep inclui um cartão Lovelace personalizado para exibição compacta de tarefas vencidas e em aberto no dashboard.

## Adicionando o cartão

No seu dashboard do Home Assistant, adicione um novo cartão e escolha **Custom: IntelliKeep Card**. Ou adicione manualmente no modo YAML:

```yaml
type: custom:intellikeep-card
title: IntelliKeep
max_tasks: 5
show_linked_entities: true
show_description: false
```

## Opções de configuração

| Opção | Tipo | Padrão | Descrição |
|---|---|---|---|
| `title` | string | `IntelliKeep` | Título do cartão exibido no cabeçalho |
| `max_tasks` | number | `5` | Número máximo de tarefas a exibir |
| `show_linked_entities` | boolean | `true` | Exibir o rótulo de área/dispositivo vinculado em cada tarefa |
| `show_description` | boolean | `false` | Exibir o texto de descrição da tarefa |
| `filter_priority` | list | — | Exibir apenas tarefas com estas prioridades: `low`, `medium`, `high`, `critical` |
| `filter_status` | list | — | Exibir apenas tarefas com estes status: `pending`, `due`, `overdue`, `completed`, `snoozed` |

## Exibição

O cartão exibe as tarefas ordenadas por urgência (vencidas primeiro, depois por data de vencimento). Cada linha de tarefa mostra:
- Barra de cor de prioridade
- Nome da tarefa
- Data de vencimento (ou rótulo "Vencida")
- Entidade vinculada (se `show_linked_entities: true`)

Clicar em uma linha de tarefa abre o detalhe completo da tarefa no painel IntelliKeep.

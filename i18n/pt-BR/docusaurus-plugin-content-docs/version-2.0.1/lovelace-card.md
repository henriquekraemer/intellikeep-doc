---
sidebar_position: 5
title: Card Lovelace
---

# Card Lovelace

O IntelliKeep vem com um card de dashboard que mostra quantas tarefas estão atrasadas e quantas vencem hoje, lista as tarefas abertas mais urgentes com uma caixa de seleção para concluí-las e leva até o painel.

<img
  src={require('@site/static/img/screenshots/card.png').default}
  alt="Card de dashboard listando uma tarefa atrasada, uma tarefa que vence hoje e duas próximas tarefas"
  className="ik-screenshot ik-screenshot--card"
/>

## Adicionando o card

Em um dashboard, clique em **Adicionar cartão** e escolha **IntelliKeep Card**. Você pode definir as opções no editor visual ou adicionar o card em YAML:

```yaml
type: custom:intellikeep-card
title: Home maintenance
max_tasks: 3
show_description: false
show_linked_entities: false
```

O card segue o idioma do seu perfil do Home Assistant (inglês, português ou espanhol).

## Opções de configuração

| Opção | Tipo | Padrão | Descrição |
|---|---|---|---|
| `title` | texto | "Manutenção da casa", no seu idioma | Título do card |
| `max_tasks` | número | `3` | Quantas tarefas listar (1–50) |
| `show_description` | booleano | `false` | Mostra a descrição de cada tarefa abaixo do nome |
| `show_linked_entities` | booleano | `false` | Mostra as áreas e os dispositivos vinculados a cada tarefa |
| `filter_priority` | lista | todas | Só em YAML. Lista apenas estas prioridades, por exemplo `[critical, high]` |
| `filter_status` | lista | tarefas abertas | Só em YAML. Lista apenas estes status: `pending`, `due`, `overdue`, `completed` |

Por exemplo, um card só para o que é urgente:

```yaml
type: custom:intellikeep-card
title: Urgent
max_tasks: 5
filter_priority: [critical, high]
filter_status: [due, overdue]
```

## O que o card mostra

- **Cabeçalho**: o título e um resumo como *1 atrasada · 1 vence hoje*, ou quantas tarefas estão abertas quando nenhuma é urgente
- **Tarefas**: as tarefas abertas, das que vencem primeiro para as que vencem depois, e então por prioridade. Cada uma tem uma caixa de seleção e a mesma etiqueta de vencimento do painel (*3 dias de atraso*, *Hoje, 19:00*, *qua., 21 de out.*)
- **Rodapé**: **Ver todas as N tarefas** abre o painel do IntelliKeep

Marcar uma caixa de seleção conclui a tarefa, registra o usuário do Home Assistant que a concluiu e mostra uma mensagem com **Desfazer**.

## Dashboards em modo YAML {/* #yaml-mode-dashboards */}

O IntelliKeep registra o recurso do card automaticamente quando os dashboards são gerenciados pela interface (modo de armazenamento, o padrão). Se os seus dashboards são configurados em YAML, adicione o recurso você mesmo:

```yaml
lovelace:
  resources:
    - url: /intellikeep_static/intellikeep-card.js
      type: module
```

Sem ele, o dashboard mostra *Custom element doesn't exist: intellikeep-card*.

:::note Mudou na 2.0
O card listava 10 tarefas e incluía as concluídas. Para voltar a esse comportamento, defina `max_tasks: 10` e `filter_status: [pending, due, overdue, completed]`. Veja [Atualizando da 1.x](./installation/upgrading).
:::

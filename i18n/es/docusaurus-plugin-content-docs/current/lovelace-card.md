---
sidebar_position: 5
title: Tarjeta Lovelace
---

# Tarjeta Lovelace

IntelliKeep incluye una tarjeta para el panel de control que muestra cuántas tareas están vencidas y cuántas vencen hoy, lista las tareas abiertas más urgentes con una casilla para completarlas y enlaza con el panel.

<img
  src={require('@site/static/img/screenshots/card.png').default}
  alt="Tarjeta del panel de control con una tarea vencida, una tarea que vence hoy y dos tareas próximas"
  className="ik-screenshot ik-screenshot--card"
/>

## Añadir la tarjeta

En un panel de control, haz clic en **Añadir tarjeta** y elige **IntelliKeep Card**. Puedes ajustar sus opciones en el editor visual o añadirla en YAML:

```yaml
type: custom:intellikeep-card
title: Home maintenance
max_tasks: 3
show_description: false
show_linked_entities: false
```

La tarjeta sigue el idioma de tu perfil de Home Assistant (inglés, portugués o español).

## Opciones de configuración

| Opción | Tipo | Predeterminado | Descripción |
|---|---|---|---|
| `title` | string | "Mantenimiento del hogar", en tu idioma | Título de la tarjeta |
| `max_tasks` | number | `3` | Cuántas tareas mostrar (1–50) |
| `show_description` | boolean | `false` | Muestra la descripción de cada tarea debajo de su nombre |
| `show_linked_entities` | boolean | `false` | Muestra las áreas y los dispositivos vinculados a cada tarea |
| `filter_priority` | list | todas | Solo en YAML. Muestra solo estas prioridades, p. ej. `[critical, high]` |
| `filter_status` | list | tareas abiertas | Solo en YAML. Muestra solo estos estados: `pending`, `due`, `overdue`, `completed` |

Por ejemplo, una tarjeta solo para lo urgente:

```yaml
type: custom:intellikeep-card
title: Urgent
max_tasks: 5
filter_priority: [critical, high]
filter_status: [due, overdue]
```

## Qué muestra la tarjeta

- **Cabecera**: el título y un resumen como *1 vencida · 1 vence hoy*, o cuántas tareas hay abiertas cuando ninguna es urgente
- **Tareas**: las tareas abiertas, primero la fecha de vencimiento más cercana y luego por prioridad. Cada una tiene una casilla y la misma etiqueta de vencimiento que el panel (*3 días de retraso*, *Hoy, 19:00*, *mié, 21 oct*)
- **Pie**: **Ver las N tareas** abre el panel de IntelliKeep

Al marcar una casilla, la tarea se completa, se registra el usuario de Home Assistant que la hizo y aparece un mensaje con **Deshacer**.

## Paneles de control en modo YAML {/* #yaml-mode-dashboards */}

IntelliKeep registra automáticamente el recurso de la tarjeta cuando los paneles de control se gestionan desde la interfaz (modo de almacenamiento, el predeterminado). Si tus paneles de control están configurados en YAML, añade el recurso tú mismo:

```yaml
lovelace:
  resources:
    - url: /intellikeep_static/intellikeep-card.js
      type: module
```

Sin él, el panel de control muestra *Custom element doesn't exist: intellikeep-card*.

:::note Cambios en la 2.0
Antes, la tarjeta mostraba 10 tareas e incluía las completadas. Para recuperar ese comportamiento, define `max_tasks: 10` y `filter_status: [pending, due, overdue, completed]`. Consulta [Actualizar desde la 1.x](./installation/upgrading).
:::

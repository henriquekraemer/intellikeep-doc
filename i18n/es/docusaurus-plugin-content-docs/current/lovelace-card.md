---
sidebar_position: 5
title: Tarjeta Lovelace
---

# Tarjeta Lovelace

IntelliKeep incluye una tarjeta Lovelace personalizada para mostrar de forma compacta las tareas vencidas y pendientes en el dashboard.

## Agregar la tarjeta

En tu dashboard de Home Assistant, agrega una nueva tarjeta y elige **Custom: IntelliKeep Card**. O agrégala manualmente en modo YAML:

```yaml
type: custom:intellikeep-card
title: IntelliKeep
max_tasks: 5
show_linked_entities: true
show_description: false
```

## Opciones de configuración

| Opción | Tipo | Por defecto | Descripción |
|---|---|---|---|
| `title` | string | `IntelliKeep` | Título de la tarjeta mostrado en el encabezado |
| `max_tasks` | number | `5` | Número máximo de tareas a mostrar |
| `show_linked_entities` | boolean | `true` | Mostrar la etiqueta de área/dispositivo vinculado en cada tarea |
| `show_description` | boolean | `false` | Mostrar el texto de descripción de la tarea |
| `filter_priority` | list | — | Mostrar solo tareas con estas prioridades: `low`, `medium`, `high`, `critical` |
| `filter_status` | list | — | Mostrar solo tareas con estos estados: `pending`, `due`, `overdue`, `completed`, `snoozed` |

## Visualización

La tarjeta muestra las tareas ordenadas por urgencia (vencidas primero, luego por fecha de vencimiento). Cada fila de tarea muestra:
- Barra de color de prioridad
- Nombre de la tarea
- Fecha de vencimiento (o etiqueta "Vencida")
- Entidad vinculada (si `show_linked_entities: true`)

Hacer clic en una fila de tarea abre el detalle completo en el panel IntelliKeep.

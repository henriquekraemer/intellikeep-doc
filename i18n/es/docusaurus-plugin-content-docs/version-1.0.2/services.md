---
sidebar_position: 6
title: Servicios
---

# Servicios

IntelliKeep expone las siguientes acciones de servicio de Home Assistant. Úsalas en automatizaciones, scripts o en el panel Herramientas del desarrollador → Acciones.

## `intellikeep.create_task`

Crea una nueva tarea.

```yaml
action: intellikeep.create_task
data:
  name: Cambiar filtro del aire acondicionado
  priority: high
  frequency: monthly
  due_date: "2025-02-01T09:00:00"
  linked_entity_ids:
    - sensor.hvac_filter
  notify_days_before: 3
  notify_on_overdue: true
```

| Campo | Requerido | Por defecto | Descripción |
|---|---|---|---|
| `name` | Sí | — | Nombre de la tarea |
| `description` | No | — | Descripción en texto libre |
| `priority` | No | `medium` | `low`, `medium`, `high`, `critical` |
| `frequency` | No | `one_time` | `one_time`, `daily`, `weekly`, `monthly`, `yearly`, `custom` |
| `custom_days_interval` | No | — | Días entre ocurrencias cuando `frequency` es `custom` |
| `due_date` | No | — | Cadena de fecha/hora ISO 8601 |
| `linked_entity_ids` | No | — | Lista de IDs de entidades de HA para asociar a la tarea |
| `notify_days_before` | No | `1` | Días antes del vencimiento para enviar un recordatorio |
| `notify_on_overdue` | No | `true` | Enviar notificación cuando la tarea venza |

## `intellikeep.complete_task`

Marca una tarea como completada y registra una entrada de ejecución. Para tareas recurrentes, la siguiente ocurrencia se programa automáticamente.

```yaml
action: intellikeep.complete_task
data:
  task_id: "<task_id>"
  completed_by: "Henrique"
  notes: "Reemplazado con un filtro MERV-13."
```

| Campo | Requerido | Descripción |
|---|---|---|
| `task_id` | Sí | ID de la tarea a completar |
| `completed_by` | No | Nombre o identificador de quien completó la tarea |
| `notes` | No | Notas opcionales de finalización |

## `intellikeep.reopen_task`

Reabre una tarea completada, marcándola como pendiente nuevamente.

```yaml
action: intellikeep.reopen_task
data:
  task_id: "<task_id>"
```

## `intellikeep.update_task`

Actualiza campos de una tarea existente. Solo se modifican los campos proporcionados.

```yaml
action: intellikeep.update_task
data:
  task_id: "<task_id>"
  priority: critical
  due_date: "2025-03-01T09:00:00"
  updated_by: "Henrique"
```

Acepta los mismos campos que `create_task`, más:

| Campo | Requerido | Descripción |
|---|---|---|
| `task_id` | Sí | ID de la tarea a actualizar |
| `enabled` | No | Activar o desactivar la tarea (`true` / `false`) |
| `updated_by` | No | Nombre o identificador de quien realizó la actualización |

## `intellikeep.delete_task`

Elimina permanentemente una tarea y su historial.

```yaml
action: intellikeep.delete_task
data:
  task_id: "<task_id>"
```

## `intellikeep.add_task_note`

Agrega una nota con marca de tiempo a una tarea existente.

```yaml
action: intellikeep.add_task_note
data:
  task_id: "<task_id>"
  content: "Se observó desgaste en la correa — monitorear el próximo mes."
  added_by: "Henrique"
```

| Campo | Requerido | Descripción |
|---|---|---|
| `task_id` | Sí | ID de la tarea a la que agregar la nota |
| `content` | Sí | Contenido en texto de la nota |
| `added_by` | No | Nombre o identificador de quien agregó la nota |

## `intellikeep.delete_task_note`

Elimina una nota específica de una tarea.

```yaml
action: intellikeep.delete_task_note
data:
  task_id: "<task_id>"
  note_id: "<note_id>"
```

| Campo | Requerido | Descripción |
|---|---|---|
| `task_id` | Sí | ID de la tarea que contiene la nota |
| `note_id` | Sí | ID de la nota a eliminar |

## `intellikeep.delete_all_data`

Elimina permanentemente todas las tareas, notas e historial de ejecuciones.

```yaml
action: intellikeep.delete_all_data
```

:::danger
Esta acción es irreversible. Todos los datos de las tareas serán eliminados permanentemente.
:::

## `intellikeep.load_sample_data`

Carga IntelliKeep con tareas de mantenimiento del hogar de ejemplo. Útil para explorar la interfaz tras una instalación nueva.

```yaml
action: intellikeep.load_sample_data
```

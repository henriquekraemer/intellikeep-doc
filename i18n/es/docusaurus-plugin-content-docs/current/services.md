---
sidebar_position: 6
title: Acciones
---

# Acciones

IntelliKeep ofrece las acciones de Home Assistant que verás a continuación. Puedes llamarlas desde automatizaciones, scripts o **Configuración → Herramientas → Acciones** (**Herramientas para desarrolladores → Acciones** en versiones anteriores de Home Assistant). El editor de acciones muestra las acciones, sus campos y sus opciones en el idioma de tu perfil (inglés, portugués o español).

Los IDs de tarea aparecen en los atributos de los [sensores](./features/notifications#sensor-entities), en los [eventos](./features/notifications#notification-event) y en los diagnósticos.

## `intellikeep.create_task`

Crea una tarea nueva.

```yaml
action: intellikeep.create_task
data:
  name: Replace HVAC filter
  icon: mdi:air-filter
  priority: high
  frequency: monthly
  repeat_interval: 3
  schedule_anchor: due_date
  due_date: "2026-12-01T09:00:00"
  linked_entity_ids:
    - area:living_room          # link to an area
    - device:abc123def456       # or a specific device ID
  notify_days_before: 3
  notify_on_overdue: true
```

| Campo | Obligatorio | Predeterminado | Descripción |
|---|---|---|---|
| `name` | Sí | — | Nombre de la tarea |
| `description` | No | — | Descripción en texto libre |
| `icon` | No | `mdi:wrench-outline` | Icono que se muestra junto a la tarea, p. ej. `mdi:air-filter` |
| `priority` | No | `medium` | `low`, `medium`, `high` o `critical` |
| `frequency` | No | `one_time` | `one_time`, `daily`, `weekly`, `monthly` o `yearly`. En las tareas recurrentes, es la unidad de `repeat_interval` |
| `repeat_interval` | No | `1` | Se repite cada N días, semanas, meses o años (1–3650) |
| `schedule_anchor` | No | `completion` | Desde qué se cuenta la próxima fecha de vencimiento: `completion` o `due_date`. Consulta [Tareas recurrentes](./features/tasks#count-the-next-due-date-from) |
| `weekdays` | No | — | En las tareas semanales: los días en que se repite, de `mon` a `sun`, p. ej. `[mon, wed, fri]` |
| `due_date` | No | — | Fecha y hora en ISO 8601. Sin desfase UTC, se interpreta en la zona horaria de Home Assistant. Si es medianoche, la tarea es de todo el día |
| `linked_entity_ids` | No | — | Áreas (`area:<area_id>`) y dispositivos (`device:<device_id>`) a los que vincular la tarea |
| `notify_days_before` | No | Valor predeterminado de la integración | Días antes de la fecha de vencimiento para enviar un recordatorio (0–365) |
| `notify_on_overdue` | No | `true` | Envía una notificación cuando la tarea pasa a estar vencida |

### Ejemplos

Una tarea semanal en días concretos. La siguiente ocurrencia siempre cae en el siguiente día seleccionado, a la misma hora, así que el calendario no se desplaza cuando completas una tarea con retraso:

```yaml
action: intellikeep.create_task
data:
  name: Take out the garbage
  icon: mdi:trash-can-outline
  frequency: weekly
  weekdays: [mon, wed, fri]
  due_date: "2026-11-09T07:00:00"
```

Una tarea cada 10 días, contando desde cada finalización:

```yaml
action: intellikeep.create_task
data:
  name: Clean the coffee machine
  frequency: daily
  repeat_interval: 10
```

:::note Frecuencia `custom` heredada
`frequency: custom` con `custom_days_interval`, de las versiones anteriores a la 2.0, sigue funcionando. Se guarda como `frequency: daily` con ese `repeat_interval`.
:::

## `intellikeep.complete_task`

Marca una tarea como hecha y registra una finalización. En las tareas recurrentes, se crea la siguiente ocurrencia.

```yaml
action: intellikeep.complete_task
data:
  task_id: "<task_id>"
  completed_by: "Henrique"
  notes: "Replaced with a MERV-13 filter."
```

| Campo | Obligatorio | Descripción |
|---|---|---|
| `task_id` | Sí | ID de la tarea que se va a completar |
| `completed_by` | No | Nombre de quien completó la tarea, que se muestra en el historial |
| `notes` | No | Notas de la finalización |

## `intellikeep.reopen_task`

Reabre una tarea completada y la deja abierta de nuevo. La finalización se deshace: su registro sale del historial y, en una tarea recurrente, se elimina la siguiente ocurrencia que había creado, salvo que ya se haya editado, tenga notas o se haya completado.

```yaml
action: intellikeep.reopen_task
data:
  task_id: "<task_id>"
  performed_by: "Henrique"
```

| Campo | Obligatorio | Descripción |
|---|---|---|
| `task_id` | Sí | ID de la tarea que se va a reabrir |
| `performed_by` | No | Nombre de quien reabrió la tarea, mostrado en el registro de actividad |

## `intellikeep.update_task`

Actualiza campos de una tarea existente. Solo cambian los campos que envíes, y el cambio queda anotado en el registro de actividad de la tarea.

```yaml
action: intellikeep.update_task
data:
  task_id: "<task_id>"
  priority: critical
  due_date: "2026-12-15T09:00:00"
  updated_by: "Henrique"
```

Acepta los mismos campos que [`create_task`](#intellikeepcreate_task), además de:

| Campo | Obligatorio | Descripción |
|---|---|---|
| `task_id` | Sí | ID de la tarea que se va a actualizar |
| `enabled` | No | `false` cierra la tarea sin registrar una finalización; `true` la vuelve a abrir. Para completar una tarea, usa [`complete_task`](#intellikeepcomplete_task) |
| `updated_by` | No | Nombre de quien hizo el cambio, que se muestra en el registro de actividad |

## `intellikeep.delete_task`

Elimina para siempre una tarea, junto con sus notas y su historial.

```yaml
action: intellikeep.delete_task
data:
  task_id: "<task_id>"
```

| Campo | Obligatorio | Descripción |
|---|---|---|
| `task_id` | Sí | ID de la tarea que se va a eliminar |

## `intellikeep.add_task_note`

Añade una nota con fecha y hora a una tarea.

```yaml
action: intellikeep.add_task_note
data:
  task_id: "<task_id>"
  content: "Noticed some wear on the belt. Check again next month."
  added_by: "Henrique"
```

| Campo | Obligatorio | Descripción |
|---|---|---|
| `task_id` | Sí | ID de la tarea a la que se añade la nota |
| `content` | Sí | Texto de la nota |
| `added_by` | No | Nombre de quien añadió la nota |

## `intellikeep.delete_task_note`

Elimina una nota de una tarea.

```yaml
action: intellikeep.delete_task_note
data:
  task_id: "<task_id>"
  note_id: "<note_id>"
```

| Campo | Obligatorio | Descripción |
|---|---|---|
| `task_id` | Sí | ID de la tarea a la que pertenece la nota |
| `note_id` | Sí | ID de la nota que se va a eliminar |

## `intellikeep.load_sample_data`

Añade un conjunto de tareas de mantenimiento del hogar de ejemplo, con iconos. Es útil para explorar el panel después de una instalación nueva.

```yaml
action: intellikeep.load_sample_data
```

## `intellikeep.delete_all_data`

Elimina para siempre todas las tareas, notas y registros de finalización. Solo los usuarios administradores pueden llamar a esta acción.

```yaml
action: intellikeep.delete_all_data
```

:::danger
Esta acción no se puede deshacer. Todos los datos de las tareas se eliminan para siempre.
:::

## Acciones de la lista de tareas pendientes

La [lista de tareas pendientes](./features/todo-and-calendar#to-do-list) también acepta las acciones `todo.*` de Home Assistant, como `todo.add_item`, `todo.update_item` y `todo.remove_item`, sobre `todo.intellikeep_tasks`.

---
sidebar_position: 5
title: Notificaciones y sensores
---

# Notificaciones y sensores

## Notificaciones

IntelliKeep te avisa cuando las tareas se acercan a su fecha de vencimiento, y otra vez cuando ya están vencidas.

### Cómo funcionan las notificaciones

- Las comprobaciones se ejecutan una vez por hora
- Se envía un recordatorio cuando una tarea entra en su ventana de **Avisar**: N días antes de la fecha de vencimiento, definidos en cada tarea (las tareas nuevas empiezan con el valor predeterminado de las [opciones de la integración](../configuration))
- Una tarea vencida recibe su propia notificación, salvo que tenga desactivado **Notificar cuando esté vencida**
- Cada tarea se notifica una vez por etapa y fecha de vencimiento. Lo que ya se envió queda guardado, así que reiniciar Home Assistant no vuelve a enviar los mismos recordatorios, y una tarea cuya fecha de vencimiento cambia recibe un recordatorio para la nueva fecha
- Completar o eliminar una tarea borra su estado de notificación
- Las notificaciones se escriben en el idioma de Home Assistant, definido en **Configuración → Sistema → Información sobre el hogar** (**General** en versiones anteriores): inglés, portugués o español, e inglés para cualquier otro idioma

### Canales de notificación

| Canal | Siempre activo | Cómo configurarlo |
|---|---|---|
| Notificaciones persistentes de Home Assistant | Sí | Vienen integradas, no hace falta configurarlas |
| Push al móvil (o cualquier acción `notify.*`) | Opcional | Define un servicio de notificación en [Configuración](../configuration#notification-service) |

### Evento de notificación {/* #notification-event */}

Cada notificación también dispara un evento `intellikeep_task_notification` que puedes usar en automatizaciones:

```yaml
triggers:
  - trigger: event
    event_type: intellikeep_task_notification
    event_data:
      event_type: overdue   # or "approaching"
```

| Campo | Descripción |
|---|---|
| `event_type` | `approaching` u `overdue` |
| `task_id` | ID de la tarea |
| `title` | Título de la notificación, en el idioma de Home Assistant |
| `message` | Mensaje de la notificación, en el idioma de Home Assistant |
| `notification_id` | ID de la notificación persistente |

### Evento de actualización de tarea

IntelliKeep también dispara `intellikeep_task_updated` cada vez que cambia una tarea, con los campos `task_id` y `action`. La acción es una de estas: `created`, `updated`, `completed`, `reopened`, `deleted`, `note_added` o `note_deleted`.

```yaml
triggers:
  - trigger: event
    event_type: intellikeep_task_updated
    event_data:
      action: completed
```

Consulta [Automatizaciones](../automations) para ver ejemplos completos.

## Entidades de sensor {/* #sensor-entities */}

IntelliKeep crea tres sensores que puedes usar en paneles de control y automatizaciones:

| Entidad | Estado | Atributos |
|---|---|---|
| `sensor.intellikeep_tasks_due_today` | Número de tareas abiertas que vencen hoy o que ya están vencidas | — |
| `sensor.intellikeep_tasks_overdue` | Número de tareas vencidas | `overdue_tasks`: lista con el `task_id`, `name`, `due_date` y `priority` de cada tarea vencida |
| `sensor.intellikeep_next_due_task` | Nombre de la tarea abierta con la fecha de vencimiento más cercana | `task_id`, `due_date`, `priority`, `linked_entity_ids`, `frequency`, `repeat_interval`, `weekdays` |

Los IDs de entidad suponen el nombre de instancia predeterminado; consulta [IDs de entidad](../configuration#entity-ids).

IntelliKeep también tiene una [entidad de lista de tareas pendientes y una entidad de calendario](./todo-and-calendar).

## Actualización de datos

El estado de las tareas se actualiza:

- Justo después de cualquier cambio hecho desde el panel, la tarjeta, la lista de tareas pendientes o una acción
- Cada 5 minutos, para que los recuentos sigan al reloj (una tarea pasa a vencer hoy o a estar vencida a la medianoche local)
- El panel y la tarjeta reciben las actualizaciones en cuanto cambian los datos, sin recargar la página

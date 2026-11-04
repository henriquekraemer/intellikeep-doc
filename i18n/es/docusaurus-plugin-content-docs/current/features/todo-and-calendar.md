---
sidebar_position: 4
title: Lista de tareas pendientes y calendario
---

# Lista de tareas pendientes y calendario

IntelliKeep añade dos entidades que llevan tus tareas a las **Listas de tareas pendientes** y al **Calendario** de Home Assistant, para que puedas verlas y completarlas fuera del panel de IntelliKeep, usarlas en otras tarjetas y crear automatizaciones con ellas.

## Lista de tareas pendientes {/* #to-do-list */}

**`todo.intellikeep_tasks`** muestra las tareas abiertas, por fecha de vencimiento, en las Listas de tareas pendientes de Home Assistant, seguidas de las tareas completadas en los últimos 30 días.

- **Marcar** un elemento completa la tarea, y una tarea recurrente recibe su siguiente ocurrencia. **Desmarcarlo** reabre la tarea y elimina esa ocurrencia, igual que **Deshacer** en el panel.
- El historial de la tarea registra el usuario de Home Assistant que marcó o desmarcó el elemento.
- Los elementos que **añades** a la lista se convierten en tareas únicas. Puedes editar su nombre, descripción y fecha de vencimiento desde la lista.
- **Eliminar** un elemento abierto elimina la tarea. Las tareas completadas conservan su historial, así que no se pueden eliminar aquí, y **Eliminar elementos completados** se rechaza. Salen de la lista 30 días después de completarse, o puedes eliminarlas desde el panel.
- Las acciones `todo.*` también funcionan, por ejemplo `todo.add_item` desde un asistente de voz o una automatización:

```yaml
action: todo.add_item
target:
  entity_id: todo.intellikeep_tasks
data:
  item: Replace the doorbell battery
  due_date: "2026-12-01"
```

Las tareas creadas así son tareas únicas con la prioridad predeterminada. Ábrelas en el panel para definir una prioridad, un icono o una repetición.

## Calendario {/* #calendar */}

**`calendar.intellikeep_tasks`** muestra cada tarea abierta en su fecha de vencimiento, incluidas las vencidas. Aparece en el **Calendario** de Home Assistant y se puede usar en las tarjetas de calendario.

- Una tarea con hora de vencimiento es un evento a esa hora. Una tarea que vence a medianoche (sin hora definida) es un evento de todo el día.
- Las tareas completadas se dejan fuera, así que una tarea hecha antes de tiempo no dispara automatizaciones a su antigua hora de vencimiento.
- Las repeticiones futuras no se proyectan: la siguiente ocurrencia aparece cuando se completa la actual, así que los disparadores de calendario solo se activan con tareas reales. La [pestaña Calendario](./calendar#future-repeats) del panel sí muestra las repeticiones futuras.
- El calendario es de solo lectura. Crea y edita las tareas en el panel o en la lista de tareas pendientes.

El estado de la entidad es `on` mientras una tarea de todo el día vence hoy, y sus atributos describen la tarea que vence hoy o la siguiente en vencer.

### Disparadores de calendario

Usa un disparador de calendario para actuar cuando vence una tarea:

```yaml
automation:
  alias: Remind me when a maintenance task is due
  triggers:
    - trigger: calendar
      event: start
      entity_id: calendar.intellikeep_tasks
  actions:
    - action: notify.mobile_app_my_phone
      data:
        title: Maintenance due
        message: "{{ trigger.calendar_event.summary }}"
```

Las tareas de todo el día empiezan a la medianoche local. El `offset` del disparador mueve la hora de activación para todas las tareas; por ejemplo, `offset: "-01:00:00"` lo activa una hora antes del vencimiento de cada tarea.

Tienes más ejemplos en [Automatizaciones](../automations).

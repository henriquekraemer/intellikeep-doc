---
sidebar_position: 3
title: Actualizar desde la 1.x
---

# Actualizar desde la 1.x

IntelliKeep 2.0 rediseñó el panel y la tarjeta del panel de control, y algunas cosas funcionan de forma distinta que en la 1.x. La mayoría de las instalaciones no necesitan cambios, pero revisa la lista de abajo antes de actualizar.

:::warning Haz primero una copia de seguridad
Haz una copia de seguridad de Home Assistant antes de actualizar. Las tareas guardadas se convierten en el primer arranque de la 2.x, y volver después a la 1.x no está soportado.
:::

## Lo que puede requerir tu atención

### La tarjeta del panel de control muestra menos tareas

La tarjeta ahora muestra **3 tareas** de forma predeterminada en lugar de 10, y deja fuera las tareas completadas. Para mantener el comportamiento anterior, añade estas opciones a la tarjeta:

```yaml
type: custom:intellikeep-card
max_tasks: 10
filter_status: [pending, due, overdue, completed]
```

Consulta [Tarjeta Lovelace](../lovelace-card) para ver todas las opciones.

### Reabrir una tarea deshace la finalización

`intellikeep.reopen_task` ahora revierte la finalización: su registro sale del historial y se elimina la siguiente ocurrencia que esa finalización creó para una tarea recurrente, salvo que alguien ya la haya editado, le haya añadido una nota o la haya completado. En la 1.x, reabrir una tarea recurrente dejaba dos ocurrencias abiertas.

Revisa cualquier automatización que reabra tareas.

### `frequency: custom` se guarda como `daily`

La antigua frecuencia **custom** con `custom_days_interval` ahora es una tarea diaria con un [`repeat_interval`](../features/tasks#recurring-tasks). Las tareas existentes se convierten cuando IntelliKeep se carga, y las acciones que todavía envían `frequency: custom` siguen funcionando.

Sin embargo, el sensor `next_due_task` y el panel ahora indican `daily`, así que tendrás que actualizar las plantillas que comparan la frecuencia con `custom`.

### La 1.x ignora los nuevos campos de las tareas

Si aun así vuelves a la 1.x, los campos añadidos en la 2.0 se ignoran: una tarea que se repite cada 3 días se repetiría todos los días, y una tarea que cuenta desde su fecha de vencimiento volvería a contar desde la finalización.

## Novedades de la 2.0

- Un panel rediseñado: tareas agrupadas por fecha de vencimiento, prioridad o área, una casilla con Deshacer y un menú ⋮ con Editar, Duplicar, Historial y Eliminar
- Tareas que se repiten cada N días, semanas, meses o años, contando desde la finalización o desde la fecha de vencimiento
- Un icono por tarea
- Una entidad de lista de tareas pendientes y una entidad de calendario para las Listas de tareas pendientes y el Calendario de Home Assistant
- Las repeticiones futuras de las tareas recurrentes en la pestaña Calendario del panel
- Una nueva pestaña Historial con quién completó cada tarea y si fue a tiempo
- Una tarjeta del panel de control rediseñada, con una casilla por tarea

La lista completa está en el [registro de cambios](https://github.com/henriquekraemer/intellikeep/blob/main/CHANGELOG.md).

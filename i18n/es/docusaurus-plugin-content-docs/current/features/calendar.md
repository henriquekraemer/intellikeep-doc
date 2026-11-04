---
sidebar_position: 2
title: Calendario
---

# Calendario

La pestaña **Calendario** organiza tus tareas por fecha de vencimiento, con un diseño que sigue el del propio calendario de Home Assistant.

<img
  src={require('@site/static/img/screenshots/calendar-desktop.png').default}
  alt="Vista de mes con tareas completadas, tareas abiertas y las repeticiones futuras de las tareas recurrentes con contorno discontinuo"
  className="ik-screenshot"
/>

## Vistas y navegación

- **Mes** y **Semana** cambian entre las dos vistas
- **Hoy**, **Anterior** y **Siguiente** te mueven entre meses o semanas, y la barra de herramientas muestra el periodo que estás viendo
- La pestaña siempre se abre en el mes actual

Los días y las semanas siguen la zona horaria y el primer día de la semana definidos en tu perfil de usuario de Home Assistant.

## Cómo se ven las tareas

- Las tareas con hora la muestran junto a un punto; las tareas de todo el día aparecen como una barra coloreada
- El color solo marca lo que requiere atención: las tareas vencidas y las que vencen hoy
- Las tareas de prioridad **Crítica** muestran el icono de su prioridad
- Las tareas completadas aparecen en gris con una marca de verificación
- Un día con más tareas de las que caben muestra **+N más**, que abre esa semana

Haz clic en una tarea para abrirla en el diálogo de la tarea. Haz clic en el espacio vacío de un día para añadir una tarea que venza ese día.

## Repeticiones futuras {/* #future-repeats */}

Las tareas recurrentes también muestran sus **repeticiones futuras**, es decir, las ocurrencias posteriores a la que está abierta, con contorno discontinuo y un icono de repetición. Haz clic en una para abrir la tarea.

Se proyectan igual que completar una tarea crea la siguiente ocurrencia, suponiendo que cada una se hace en su fecha de vencimiento (y una vencida, hoy). Por eso son exactas en las tareas que cuentan desde su fecha de vencimiento, y solo una estimación en las que cuentan desde la finalización, cuyas fechas reales dependen de cuándo se haga cada ocurrencia.

El interruptor **Mostrar repeticiones futuras**, en **Filtros**, permite ocultarlas.

:::note
Las repeticiones futuras solo aparecen en el panel. La entidad [`calendar.intellikeep_tasks`](./todo-and-calendar#calendar) muestra solo las ocurrencias abiertas, así que los disparadores de calendario solo se activan con tareas reales.
:::

## Filtrar

**Filtros** tiene los mismos filtros de área, dispositivo y prioridad que la pestaña [Tareas](./tasks#search-and-filters), además del interruptor de las repeticiones futuras.

## En el teléfono

En el teléfono, el mes es una cuadrícula pequeña con un punto por tarea, y las tareas del día elegido aparecen debajo. La vista de semana es una lista de días.

<img
  src={require('@site/static/img/screenshots/calendar-mobile.png').default}
  alt="Calendario mensual en un teléfono con las tareas del día elegido debajo"
  className="ik-screenshot ik-screenshot--phone"
/>

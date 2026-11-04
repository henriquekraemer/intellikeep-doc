---
sidebar_position: 1
slug: /
title: Introducción
---

# IntelliKeep

IntelliKeep es una integración personalizada para Home Assistant, gratuita y de código abierto, que lleva el control de las tareas de mantenimiento de tu casa. Lo reúne todo en un solo lugar, desde el cambio mensual de un filtro hasta la revisión anual de la caldera, y te avisa antes de que algo venza. Cada tarea guarda su propio historial, así que siempre sabes qué se hizo, quién lo hizo y cuándo.

<img
  src={require('@site/static/img/screenshots/tasks-desktop.png').default}
  alt="Panel de IntelliKeep con las tareas abiertas agrupadas en Vencidas, Hoy, Esta semana y Más adelante"
  className="ik-screenshot"
/>

## Qué hace IntelliKeep

- Tareas únicas y recurrentes que se repiten cada N días, semanas, meses o años, contando desde la finalización o desde la fecha de vencimiento
- Tareas semanales fijadas en días concretos de la semana, como la recogida de basura los Lun/Mié/Vie
- Cuatro niveles de prioridad (baja, media, alta, crítica), que se muestran con un icono y una etiqueta
- Un icono por tarea, elegido entre los Material Design Icons
- Vínculos con áreas de Home Assistant o con dispositivos concretos
- Notas con fecha y hora en cada tarea, con el nombre de quien las escribió
- Un registro de actividad por tarea con las ediciones, finalizaciones, reaperturas y cambios en las notas
- Un calendario con vistas de mes y de semana, las repeticiones futuras de las tareas recurrentes y filtros por área, dispositivo y prioridad
- Un historial de finalizaciones con quién hizo cada tarea y si fue a tiempo, además de exportación a CSV e impresión
- Recordatorios mediante las notificaciones persistentes de Home Assistant, con notificaciones push opcionales al móvil
- Tres sensores: `tasks_due_today`, `tasks_overdue` y `next_due_task`
- Una lista de tareas pendientes (`todo.intellikeep_tasks`) para las Listas de tareas pendientes de Home Assistant y un calendario (`calendar.intellikeep_tasks`) para su Calendario, las tarjetas de calendario y los disparadores de calendario
- Una tarjeta para el panel de control que muestra las tareas más urgentes y las completa con un clic
- Un panel adaptable que sigue la interfaz de Home Assistant en el escritorio y en el teléfono, en inglés, portugués y español

## Qué no hace IntelliKeep

- Detección automática de dispositivos
- Actualizaciones de firmware de los fabricantes
- Autenticación con cuentas externas ni sincronización con plataformas de tareas de terceros

## Inicio rápido

1. [Instala mediante HACS](./installation/hacs) (recomendado)
2. Reinicia Home Assistant
3. Añade la integración en **Configuración → Dispositivos y servicios**
4. Abre el panel de IntelliKeep en la barra lateral y crea tu primera tarea

:::tip ¿Vienes de la 1.x?
La versión 2.0 rediseñó el panel y la tarjeta del panel de control, y cambió algunos valores predeterminados. Lee [Actualizar desde la 1.x](./installation/upgrading) antes de actualizar.
:::

---
sidebar_position: 3
title: Configuración
---

# Configuración

## Configuración inicial

En el asistente de configuración de la integración puedes definir:

| Opción | Predeterminado | Descripción |
|---|---|---|
| **Nombre de la instancia** | `IntelliKeep` | Nombre del dispositivo de IntelliKeep en Home Assistant. Los IDs de entidad se forman a partir de él |
| **Tiempo de antelación predeterminado para notificaciones (días)** | `1` | Cuántos días antes de la fecha de vencimiento se envía un recordatorio (0–30). Las tareas nuevas empiezan con este valor, y cada tarea puede cambiarlo |
| **Servicio de notificación** | *(vacío)* | Acción `notify.*` opcional, por ejemplo `notify.mobile_app_my_phone` |

Solo se puede configurar una instancia de IntelliKeep por instalación de Home Assistant.

## Cambiar la configuración más adelante

Puedes cambiar todas las opciones después de la instalación:

1. Ve a **Configuración → Dispositivos y servicios**
2. Busca la entrada **IntelliKeep**
3. Haz clic en **Configurar** para ajustar las opciones, o elige **Reconfigurar** en el menú ⋮ para volver a pasar por el asistente de configuración

IntelliKeep se recarga una vez con la nueva configuración.

## Servicio de notificación {/* #notification-service */}

Deja **Servicio de notificación** vacío si solo quieres las notificaciones persistentes de Home Assistant (el icono de la campana en la interfaz).

Para recibir también notificaciones push en el móvil, escribe el nombre de una acción `notify.*`. Encontrarás las disponibles en tu instalación en **Configuración → Herramientas → Acciones** (**Herramientas para desarrolladores → Acciones** en versiones anteriores de Home Assistant).

Valores de ejemplo:
- `notify.mobile_app_my_phone`
- `notify.all_devices`

Consulta [Notificaciones y sensores](./features/notifications) para saber cuándo se envían los recordatorios.

## IDs de entidad {/* #entity-ids */}

IntelliKeep crea un dispositivo, con el nombre definido en **Nombre de la instancia**, que tiene estas entidades:

| Entidad | Descripción |
|---|---|
| `sensor.intellikeep_tasks_due_today` | Tareas que vencen hoy o que ya están vencidas |
| `sensor.intellikeep_tasks_overdue` | Tareas vencidas |
| `sensor.intellikeep_next_due_task` | La próxima tarea en vencer |
| `todo.intellikeep_tasks` | [Lista de tareas pendientes](./features/todo-and-calendar#to-do-list) con las tareas abiertas y las completadas recientemente |
| `calendar.intellikeep_tasks` | [Calendario](./features/todo-and-calendar#calendar) con las tareas abiertas en sus fechas de vencimiento |

Los IDs de arriba suponen el nombre de instancia predeterminado. Con otro nombre, la parte `intellikeep` cambia con él (por ejemplo, `todo.home_tasks` para una instancia llamada *Home*).

## Idioma, fechas y horas

El panel y la tarjeta del panel de control siguen el idioma configurado en tu perfil de usuario de Home Assistant (están disponibles inglés, portugués y español, y el inglés se usa si tu idioma no está). Las fechas y horas siguen el idioma, la zona horaria, el primer día de la semana y el formato de 12/24 horas del perfil.

Las tareas pasan a vencer hoy, y después a estar vencidas, a la medianoche local, en la zona horaria de Home Assistant.

## Configuración del panel

El icono del engranaje en la cabecera del panel abre la configuración propia del panel:

- **Animaciones de tareas**: desactiva las transiciones al completar, eliminar, reabrir o moverte entre tareas. Se guarda en cada navegador.
- **Eliminar todos los datos**: elimina para siempre todas las tareas, notas y registros de finalización. Pide confirmación, y solo los usuarios administradores ven este botón.

Debajo de la configuración, el panel muestra las acciones, los eventos y los IDs de entidad de IntelliKeep en tu instalación, y el archivo donde se guardan los datos.

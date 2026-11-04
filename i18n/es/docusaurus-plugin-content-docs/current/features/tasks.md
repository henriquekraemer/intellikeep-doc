---
sidebar_position: 1
title: Tareas
---

# Tareas

La pestaña **Tareas** es la vista principal del panel de IntelliKeep. Muestra tus tareas, te permite completarlas con un clic y abre el diálogo de la tarea para crearlas o editarlas.

<img
  src={require('@site/static/img/screenshots/tasks-desktop.png').default}
  alt="Tareas abiertas agrupadas en Vencidas, Hoy, Esta semana y Más adelante, cada una con una casilla, un icono, la prioridad y la fecha de vencimiento"
  className="ik-screenshot"
/>

## La lista de tareas

En la parte superior de la lista eliges entre:

- **Abiertas**: todas las tareas que aún quedan por hacer
- **Completadas**: las tareas completadas en los últimos 30 días, de la más reciente a la más antigua (las anteriores siguen en la pestaña [Historial](./history))

De forma predeterminada, las tareas abiertas se agrupan por fecha de vencimiento: **Vencidas**, **Hoy**, **Esta semana**, **Más adelante** y **Sin fecha de vencimiento**. Con **Agrupar por** puedes agruparlas por **Prioridad** o por **Área**, o quitar la agrupación. La elección se recuerda en el navegador.

Cada fila muestra el icono de la tarea, su nombre y número (`#001`), su descripción, la prioridad y una etiqueta de vencimiento como *3 días de retraso*, *Hoy, 19:00* o *sáb, 7 nov*. El rojo y el ámbar se reservan para lo que requiere atención: las tareas vencidas, las que vencen hoy y la prioridad **Crítica**.

### Completar una tarea

Marca la casilla de una tarea para completarla. Aparece el mensaje *Tarea completada* con **Deshacer**, que reabre la tarea al instante. Completar una tarea recurrente crea su siguiente ocurrencia (consulta [Tareas recurrentes](#recurring-tasks)).

El nombre del usuario de Home Assistant que completó la tarea queda registrado en su historial.

### El menú ⋮

Cada tarea tiene un menú ⋮ con:

- **Editar**: abre el diálogo de la tarea
- **Duplicar**: abre el formulario de tarea nueva con los mismos campos ya rellenados
- **Historial**: abre el diálogo de la tarea en su pestaña Historial
- **Eliminar**: elimina la tarea, tras pedir confirmación

### Búsqueda y filtros {/* #search-and-filters */}

- La **búsqueda** encuentra tareas por nombre, descripción o número
- **Filtros** acota la lista por **prioridad**, **área** y **dispositivo**. Cuando filtras a la vez por área y por dispositivo, puedes combinarlos como *Área O dispositivo* o *Área Y dispositivo*

Al seleccionar un área, el selector de dispositivos se limita a los dispositivos de esa área. Los filtros activos aparecen como etiquetas que puedes quitar una a una o todas a la vez, y se recuerdan en el navegador.

### En el teléfono

En teléfonos y ventanas estrechas (de menos de 600px de ancho, o cuando Home Assistant oculta la barra lateral), el panel se adapta:

- Las pestañas Tareas, Calendario e Historial ocupan todo el ancho, y la búsqueda pasa a una lupa en la cabecera
- Cada fila conserva solo la casilla y el nombre, con la fecha de vencimiento, la prioridad y la repetición en una línea debajo
- **Agrupar por** pasa a **Filtros**, y **Agregar tarea** se convierte en un botón flotante

<img
  src={require('@site/static/img/screenshots/tasks-mobile.png').default}
  alt="Lista de tareas en un teléfono"
  className="ik-screenshot ik-screenshot--phone"
/>

## Crear y editar una tarea

Haz clic en **Agregar tarea**, en la barra de herramientas de la lista, para crear una tarea. Haz clic en una tarea, o elige **Editar** en su menú ⋮, para abrirla. También puedes crear tareas con la acción [`intellikeep.create_task`](../services#intellikeepcreate_task) o desde la [lista de tareas pendientes](./todo-and-calendar#to-do-list) de Home Assistant.

<img
  src={require('@site/static/img/screenshots/dialog-desktop.png').default}
  alt="Diálogo de la tarea con el nombre, el icono, la prioridad, la fecha y hora de vencimiento y cada cuánto se repite la tarea"
  className="ik-screenshot"
/>

La cabecera del diálogo muestra el nombre de la tarea, su número y cómo se repite, además de un menú ⋮ con **Duplicar** y **Eliminar**. Una tarea existente tiene tres pestañas: **Detalles**, **Notas** e **Historial**. En el pie están **Completar**, **Cancelar** y **Guardar**.

### Campos de la tarea

| Campo | Descripción |
|---|---|
| **Nombre** | Título de la tarea (obligatorio) |
| **Icono** | Cualquier icono de Material Design, elegido con el selector de iconos de Home Assistant (busca por nombre o por palabra clave). Las tareas sin icono muestran una llave inglesa (`mdi:wrench-outline`) |
| **Descripción** | Texto libre opcional |
| **Prioridad** | **Baja**, **Media**, **Alta** o **Crítica** |
| **Fecha de vencimiento** y **Hora** | Cuándo vence la tarea (en las tareas recurrentes, el campo se llama **Próximo vencimiento**). La **×** junto a la hora la quita y convierte la tarea en una tarea de *todo el día* |
| **Repetición** | *No se repite*, o *Repetir cada N días, semanas, meses o años* |
| **Repetir el** | En las tareas semanales: los días de la semana en que se repite |
| **Contar el próximo vencimiento desde la** | En las tareas recurrentes: **Fecha de finalización** o **Fecha de vencimiento original** (ver más abajo) |
| **Vinculada a** | Áreas y dispositivos de Home Assistant, que se muestran como etiquetas que puedes quitar. Los filtros de área y de dispositivo usan estos vínculos |
| **Avisar** | Cuántos días antes de la fecha de vencimiento se envía el recordatorio. Las tareas nuevas empiezan con el [valor predeterminado de las opciones de la integración](../configuration) |
| **Notificar cuando esté vencida** | Envía una notificación cuando la tarea pasa a estar vencida |

### Tareas de todo el día

Una fecha de vencimiento sin hora es una tarea de todo el día. Se guarda como medianoche, igual que las fechas que defines desde el calendario y desde las Listas de tareas pendientes de Home Assistant. Si vence hoy, una tarea así muestra **Hoy** en lugar de *Hoy, 0:00*, y el diálogo de la tarea muestra su hora como **Todo el día**.

## Tareas recurrentes {/* #recurring-tasks */}

Cuando completas una tarea recurrente, IntelliKeep registra la finalización y crea la siguiente ocurrencia, con un número de tarea nuevo y el mismo nombre, icono, prioridad, vínculos y configuración de notificaciones. Cada ocurrencia conserva sus propias notas e historial, y la pestaña Historial del diálogo de la tarea muestra las ocurrencias anteriores.

### Repetir cada N periodos

Una tarea se repite cada N **días**, **semanas**, **meses** o **años**. Por ejemplo, *Repetir cada 3 meses* para el filtro del aire acondicionado, o *Repetir cada 2 semanas* para limpiar el refrigerador.

Las repeticiones mensuales y anuales mantienen el día del mes y, en los meses más cortos, pasan al último día: una tarea que vence el 31 de enero y se repite cada mes vence el 28 (o el 29) de febrero.

### Desde cuándo se cuenta el próximo vencimiento {/* #count-the-next-due-date-from */}

La opción **Contar el próximo vencimiento desde la** decide a partir de qué fecha se calcula la siguiente fecha de vencimiento:

- **Fecha de finalización** (la predeterminada): se cuenta desde el momento en que haces la tarea. Si completas una tarea mensual con 5 días de retraso, la siguiente también se retrasa 5 días. Ideal para cosas que se desgastan con el tiempo, como un filtro.
- **Fecha de vencimiento original**: se cuenta desde la propia fecha de vencimiento de la tarea, lo que mantiene un calendario fijo. Los periodos que ya pasaron se saltan, así que completar con retraso nunca crea una tarea que nazca ya vencida. Ideal para cosas ligadas al calendario, como una inspección anual en marzo.

### Días concretos de la semana

Una tarea semanal puede repetirse en los días que elijas, por ejemplo la recogida de basura los **Lun**, **Mié** y **Vie**. La siguiente ocurrencia es el siguiente día seleccionado, a la hora original de la tarea, así que el calendario no se desplaza cuando completas una tarea con retraso. Con *Repetir cada 2 semanas*, la tarea se repite en los días seleccionados una semana sí y otra no.

Si no hay ningún día seleccionado, una tarea semanal se repite cada 7 días (o cada N semanas) desde la última finalización.

:::note
En las versiones anteriores a la 2.0, los intervalos en días usaban la frecuencia **custom**. Esas tareas ahora son tareas diarias con un intervalo de repetición y se comportan igual. Consulta [Actualizar desde la 1.x](../installation/upgrading).
:::

## Estado de la tarea

| Estado | Significado |
|---|---|
| `pending` | Abierta, vence más adelante (o no tiene fecha de vencimiento) |
| `due` | Abierta, vence hoy |
| `overdue` | Abierta, y la fecha de vencimiento ya pasó. Las tareas pasan a estar vencidas el día después de su fecha de vencimiento, a la medianoche local |
| `completed` | Hecha. Las tareas completadas son de solo lectura hasta que las reabres |

El estado se calcula a partir de la fecha de vencimiento, en la zona horaria de Home Assistant, y nunca se guarda.

## Notas

La pestaña **Notas** del diálogo de la tarea reúne las notas sobre la tarea. Cada nota lleva fecha y hora y registra el usuario de Home Assistant que la añadió. Puedes añadir y eliminar notas ahí, o con las acciones [`intellikeep.add_task_note`](../services#intellikeepadd_task_note) y [`intellikeep.delete_task_note`](../services#intellikeepdelete_task_note).

## Historial y registro de actividad de la tarea

La pestaña **Historial** del diálogo de la tarea muestra:

- Cada finalización de la tarea, con quién la completó, cuándo y si fue con retraso
- Las ocurrencias anteriores de una tarea recurrente
- El **Registro de actividad**: cada edición (con los campos que cambiaron), finalización, reapertura y nota añadida o eliminada

## Reabrir una tarea {/* #reopening-a-task */}

Abre una tarea completada y haz clic en **Reabrir**, usa **Deshacer** justo después de completarla, o desmárcala en la [lista de tareas pendientes](./todo-and-calendar#to-do-list). Reabrir deshace la finalización: su registro sale del historial y se elimina la siguiente ocurrencia que creó para una tarea recurrente, salvo que alguien ya la haya editado, le haya añadido una nota o la haya completado.

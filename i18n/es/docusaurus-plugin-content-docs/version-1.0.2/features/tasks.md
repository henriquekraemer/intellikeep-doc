---
sidebar_position: 1
title: Tareas
---

# Tareas

La vista de Tareas es el panel principal de IntelliKeep. Muestra todas las tareas pendientes y completadas con filtros y búsqueda avanzados.

## Crear una tarea

Las tareas pueden crearse desde la interfaz del panel o mediante la acción de servicio [`intellikeep.create_task`](../services#intellikeepcreate_task).

### Campos de la tarea

| Campo | Descripción |
|---|---|
| **Nombre** | Título de la tarea |
| **Prioridad** | `baja`, `media`, `alta` o `crítica` |
| **Fecha de vencimiento** | Cuándo vence la tarea |
| **Frecuencia** | Recurrencia: `one_time`, `daily`, `weekly`, `monthly`, `yearly` o `custom` (con `custom_days_interval`) |
| **Entidades vinculadas** | Áreas de HA o IDs de dispositivos específicos |
| **Notificar N días antes** | Sobreescribe el tiempo global de notificación para esta tarea |
| **Descripción** | Descripción en texto libre (opcional) |

## Tareas recurrentes

Cuando se completa una tarea recurrente, se crea automáticamente una nueva instancia con la próxima fecha de vencimiento calculada según la frecuencia configurada.

Frecuencias soportadas:
- `one_time` — sin recurrencia
- `daily`
- `weekly`
- `monthly`
- `yearly`
- `custom` — especifica el número de días mediante `custom_days_interval`

## Niveles de prioridad

Las prioridades se muestran como una barra de color en cada tarjeta de tarea:

| Prioridad | Color |
|---|---|
| Baja | Verde |
| Media | Amarillo |
| Alta | Naranja |
| Crítica | Rojo |

## Filtros y búsqueda

La vista de Tareas soporta filtros por:
- **Área** — mostrar tareas vinculadas a un área específica de HA
- **Dispositivo** — mostrar tareas vinculadas a un dispositivo específico
- **Prioridad** — filtrar por uno o más niveles de prioridad
- **Búsqueda por texto** — filtrar por nombre de tarea

## Notas

Cada tarea tiene una sección de Notas dedicada. Las notas llevan marca de tiempo y registran el autor (usuario de HA que las agregó). Las notas pueden agregarse, visualizarse y eliminarse desde la vista de detalle de la tarea.

## Log de actividad

Cada cambio en una tarea queda registrado en su Log de Actividad:
- Campos editados
- Tarea completada (con marca de tiempo de finalización)
- Tarea reabierta
- Notas agregadas o eliminadas

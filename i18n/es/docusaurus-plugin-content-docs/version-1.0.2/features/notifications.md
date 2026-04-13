---
sidebar_position: 4
title: Notificaciones y Sensores
---

# Notificaciones y Sensores

## Notificaciones

IntelliKeep envía recordatorios cuando las tareas están próximas a vencer o ya han vencido.

### Cómo funcionan las notificaciones

- Las verificaciones de notificación se ejecutan **cada hora**
- Se envía un recordatorio **N días antes** de la fecha de vencimiento de la tarea (configurable globalmente y por tarea)
- Las tareas vencidas también generan una notificación
- La deduplicación de notificaciones es en memoria y se reinicia al reiniciar HA

### Canales de notificación

| Canal | Siempre activo | Cómo configurar |
|---|---|---|
| Notificaciones persistentes de HA | Sí | Integrado, sin configuración necesaria |
| Push móvil | Opcional | Configura un servicio `notify.*` en [Configuración](../configuration) |

### Disparador de automatización

IntelliKeep lanza un evento que puedes usar en automatizaciones de HA:

```yaml
triggers:
  - trigger: event
    event_type: intellikeep_task_notification
    event_data:
      event_type: overdue   # o "approaching"
```

Campos de datos del evento disponibles: `task_id`, `title`, `message`, `event_type`.

## Entidades sensor

IntelliKeep crea tres entidades sensor que puedes usar en dashboards y automatizaciones:

| Entidad | Descripción |
|---|---|
| `sensor.intellikeep_tasks_due_today` | Número de tareas que vencen hoy |
| `sensor.intellikeep_tasks_overdue` | Número de tareas actualmente vencidas |
| `sensor.intellikeep_next_due_task` | Nombre y fecha de vencimiento de la próxima tarea |

El estado de los sensores se actualiza:
- Inmediatamente después de cualquier acción de servicio que cambie los datos de las tareas
- Cada 5 minutos mediante la actualización programada del coordinador

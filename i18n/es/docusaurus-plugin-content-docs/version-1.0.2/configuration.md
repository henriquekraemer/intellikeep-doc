---
sidebar_position: 3
title: Configuración
---

# Configuración

## Configuración inicial

Durante el asistente de configuración de la integración puedes definir:

| Opción | Por defecto | Descripción |
|---|---|---|
| **Nombre de la instancia** | `IntelliKeep` | Etiqueta mostrada en Home Assistant |
| **Notificar N días antes** | `1` | Días antes del vencimiento de la tarea para enviar un recordatorio |
| **Servicio de notificación** | *(vacío)* | Servicio `notify.*` opcional, ej.: `notify.mobile_app_mi_telefono` |

## Cambiar la configuración después

Todas las opciones pueden actualizarse tras la instalación:

1. Ve a **Configuración → Dispositivos y Servicios**
2. Encuentra la entrada **IntelliKeep**
3. Haz clic en **Configurar** para ajustar los ajustes, o **Reconfigurar** para ejecutar el asistente nuevamente

## Servicio de notificación

Deja el campo **Servicio de notificación** vacío para usar solo las notificaciones persistentes de Home Assistant (el ícono de campana en la interfaz de HA).

Para recibir también notificaciones push en el móvil, ingresa un nombre de servicio `notify.*`. Puedes encontrar los servicios disponibles en **Herramientas del desarrollador → Acciones**.

Ejemplos:
- `notify.mobile_app_mi_telefono`
- `notify.all_devices`

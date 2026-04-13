---
sidebar_position: 8
title: Solución de Problemas
---

# Solución de Problemas

## El panel o la tarjeta no muestran datos actuales

1. Ve a **Configuración → Dispositivos y Servicios** y confirma que la entrada IntelliKeep está cargada y no muestra errores
2. Descarga el **Diagnóstico** de la entrada de configuración y verifica que los contadores de tareas coincidan con lo esperado
3. Si reconstruiste o actualizaste el frontend recientemente, **reinicia Home Assistant** para recargar los assets estáticos

## Las notificaciones móviles no llegan

1. En **Herramientas del desarrollador → Acciones**, verifica que el servicio `notify.*` configurado realmente exista
2. Deja el campo **Servicio de notificación** vacío para usar solo las notificaciones persistentes de HA
3. Revisa los **logs de Home Assistant** para errores relacionados con IntelliKeep (filtra por `intellikeep`)

## Las tareas aparecen vencidas inesperadamente

1. Verifica la **hora del sistema y zona horaria** de Home Assistant — IntelliKeep usa la hora del sistema de HA
2. Confirma el valor de `due_date` almacenado en el diagnóstico de la tarea
3. Abre el **Log de actividad** de la tarea para ver si fue completada y luego reabierta

## La integración falla al cargar tras una actualización

1. Limpia el caché del navegador y recarga
2. Revisa los logs para errores de importación Python relacionados con `custom_components.intellikeep`
3. Asegúrate de que todo el directorio `custom_components/intellikeep/` fue reemplazado (no solo algunos archivos)
4. Si usas HACS, vuelve a descargar la integración y reinicia

## Limitaciones conocidas

- IntelliKeep es de **instancia única** — solo una entrada de integración por instancia de Home Assistant
- Los datos de las tareas se almacenan localmente y no se comparten entre instancias de HA
- La deduplicación de notificaciones es en memoria y **se reinicia tras un reinicio de HA**
- Los sensores resumen el estado de las tareas; no se crean entidades individuales por tarea

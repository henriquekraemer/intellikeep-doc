---
sidebar_position: 8
title: Solución de problemas
---

# Solución de problemas

## El panel o la tarjeta no muestran los datos actuales

1. Ve a **Configuración → Dispositivos y servicios** y confirma que la entrada de IntelliKeep está cargada y no muestra errores
2. Usa **Descargar diagnósticos** en la entrada de configuración y comprueba que los contadores de tareas tienen sentido
3. Si acabas de actualizar IntelliKeep, **reinicia Home Assistant** y recarga la página del navegador (vacía su caché si hace falta) para cargar los nuevos archivos del frontend

## "Custom element doesn't exist: intellikeep-card"

El panel de control no encuentra el código de la tarjeta.

1. Si tus paneles de control están configurados en YAML, añade el recurso de la tarjeta a mano, como se explica en [Paneles de control en modo YAML](./lovelace-card#yaml-mode-dashboards)
2. Si no, comprueba en **Configuración → Paneles de control → ⋮ → Recursos** que aparece `/intellikeep_static/intellikeep-card.js`, reinicia Home Assistant y recarga la página

## No llegan las notificaciones al móvil

1. En **Configuración → Herramientas → Acciones** (**Herramientas para desarrolladores → Acciones** en versiones anteriores de Home Assistant), comprueba que la acción `notify.*` que configuraste existe de verdad
2. Deja vacío el campo **Servicio de notificación** para usar solo las notificaciones persistentes
3. Revisa los **registros de Home Assistant** en busca de errores de IntelliKeep (filtra por `intellikeep`)
4. Recuerda que cada tarea se notifica una vez por etapa hasta que Home Assistant se reinicia

## Aparecen tareas vencidas sin motivo aparente

1. Revisa la **zona horaria** de Home Assistant en **Configuración → Sistema → Información sobre el hogar** (**General** en versiones anteriores). Las tareas pasan a vencer hoy, y después a estar vencidas, a la medianoche en esa zona horaria
2. Revisa la zona horaria de tu **perfil de usuario**: las fechas del panel la siguen
3. Confirma el valor guardado de `due_date` en los diagnósticos de la tarea
4. Abre la pestaña **Historial** de la tarea para ver si se completó y luego se reabrió

## Una tarea recurrente recibió una fecha siguiente inesperada

1. Revisa **Contar el próximo vencimiento desde la** en el diálogo de la tarea. Con **Fecha de finalización**, una finalización con retraso también mueve la siguiente ocurrencia; con **Fecha de vencimiento original**, la tarea mantiene un calendario fijo
2. En las tareas semanales con días seleccionados, la siguiente ocurrencia es el siguiente día seleccionado después de la fecha de vencimiento actual, a la hora original de la tarea
3. En la pestaña Calendario del panel, las fechas de las repeticiones futuras son una estimación en las tareas que cuentan desde la finalización

## La integración no carga después de una actualización

1. Revisa los registros en busca de errores de Python relacionados con `custom_components.intellikeep`
2. Asegúrate de que se reemplazó todo el directorio `custom_components/intellikeep/`, no solo algunos archivos
3. Si usas HACS, vuelve a descargar la integración y reinicia
4. Comprueba que tienes Home Assistant 2026.1 o posterior

## Limitaciones conocidas

- IntelliKeep es de instancia única: solo se permite una entrada de la integración por instalación de Home Assistant
- Los datos de las tareas se guardan en local (en `.storage/intellikeep`) y no se comparten entre instalaciones de Home Assistant
- Las tareas no son entidades individuales: los sensores las resumen, y la lista de tareas pendientes y el calendario las enumeran
- La entidad `calendar.intellikeep_tasks` solo muestra la ocurrencia actual de cada tarea recurrente. La pestaña Calendario del panel proyecta las siguientes y, en las tareas que cuentan desde la finalización, esas fechas son una estimación
- La deduplicación de notificaciones se guarda en memoria y se pierde cuando Home Assistant se reinicia

## Desinstalar IntelliKeep

1. Ve a **Configuración → Dispositivos y servicios**
2. Abre **IntelliKeep** y elige **Eliminar**
3. Quita las tarjetas del panel de control y las automatizaciones que todavía usen acciones, entidades o eventos de IntelliKeep
4. Si lo instalaste a mano, elimina `custom_components/intellikeep/` del directorio de configuración de Home Assistant

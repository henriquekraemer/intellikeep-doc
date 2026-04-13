---
sidebar_position: 1
slug: /
title: Introducción
---

# IntelliKeep

**IntelliKeep** es un sistema de gestión de tareas de mantenimiento del hogar, creado como una integración personalizada gratuita y de código abierto para Home Assistant. Centraliza todas las tareas del hogar — desde simples cambios de filtros hasta revisiones periódicas — ofreciendo alertas automáticas y un historial completo de tareas.

## Qué hace IntelliKeep

- Crear **tareas únicas o recurrentes** (diaria, semanal, mensual, anual o intervalo personalizado)
- Definir **niveles de prioridad** (baja, media, alta, crítica) con indicadores visuales por color
- Vincular tareas a **áreas de Home Assistant o dispositivos específicos**
- Agregar **notas con marca de tiempo** y registro de autor por tarea
- Registrar un **log de actividad** completo de cada edición, finalización y reapertura
- Visualizar tareas en un **Calendario** (semana/mes) con filtros por área, dispositivo y prioridad
- Consultar un **Historial de Ejecuciones** completo con exportación CSV y soporte de impresión
- Recibir **notificaciones** mediante notificaciones persistentes de HA o push móvil opcional
- Monitorear el estado de tareas mediante tres **entidades sensor**: `tasks_due_today`, `tasks_overdue`, `next_due_task`
- Mostrar tareas vencidas y pendientes en el dashboard de HA usando la **tarjeta Lovelace**

## Qué no hace IntelliKeep

- Descubrimiento automático de dispositivos
- Actualizaciones de firmware de fabricantes
- Autenticación de cuenta externa ni sincronización con plataformas de tareas de terceros

## Inicio rápido

1. [Instalar mediante HACS](./installation/hacs) (recomendado)
2. Reiniciar Home Assistant
3. Agregar la integración en **Configuración → Dispositivos y Servicios**
4. Abrir el **panel IntelliKeep** en la barra lateral de HA y crear la primera tarea

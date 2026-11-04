---
sidebar_position: 1
title: Instalar mediante HACS
---

# Instalar mediante HACS

HACS (Home Assistant Community Store) es el método de instalación recomendado. Además, te avisa cuando sale una versión nueva.

## Requisitos previos

- [HACS](https://hacs.xyz) instalado en tu instancia de Home Assistant
- Home Assistant 2026.1 o posterior

## Pasos

1. Abre **HACS** en la barra lateral de Home Assistant
2. Haz clic en el menú de tres puntos (⋮) de la esquina superior derecha → **Repositorios personalizados**
3. Añade la URL del repositorio:
   ```
   https://github.com/henriquekraemer/intellikeep
   ```
   Elige **Integración** como tipo y haz clic en **Añadir**
4. Busca **IntelliKeep** en HACS y haz clic en **Descargar**
5. **Reinicia Home Assistant**
6. Ve a **Configuración → Dispositivos y servicios → Añadir integración**
7. Busca **IntelliKeep** y sigue el asistente de configuración

Al terminar, el **panel de IntelliKeep** aparece en la barra lateral de Home Assistant, y la [tarjeta del panel de control](../lovelace-card) queda lista para añadirla a cualquier panel de control.

## Actualizar

Cuando HACS muestre una actualización de IntelliKeep, descárgala y reinicia Home Assistant. Lee antes el [registro de cambios](https://github.com/henriquekraemer/intellikeep/blob/main/CHANGELOG.md) y, si pasas de la 1.x a la 2.x, lee [Actualizar desde la 1.x](./upgrading).

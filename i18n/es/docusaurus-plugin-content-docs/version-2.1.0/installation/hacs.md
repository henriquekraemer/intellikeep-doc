---
sidebar_position: 1
title: Instalar mediante HACS o el Marketplace
---

# Instalar mediante HACS o el Marketplace

IntelliKeep está en la lista predeterminada de HACS, así que lo encuentras con una búsqueda, sin añadir un repositorio personalizado. Home Assistant 2026.11 y posteriores incluyen el **Marketplace**, que instala desde el mismo catálogo. En versiones anteriores, usa [HACS](https://hacs.xyz). Cualquiera de los dos es el método de instalación recomendado, y ambos te avisan cuando sale una versión nueva.

## Requisitos previos

- Home Assistant 2026.1 o posterior
- Antes de Home Assistant 2026.11, [HACS](https://hacs.xyz) instalado en tu instancia de Home Assistant

## Abrir IntelliKeep directamente

[![Abrir IntelliKeep en el Marketplace de tu instancia de Home Assistant.](https://my.home-assistant.io/badges/marketplace_repository.svg)](https://my.home-assistant.io/redirect/marketplace_repository/?owner=henriquekraemer&repository=intellikeep&category=integration)

El botón abre IntelliKeep en el Marketplace, o en HACS antes de Home Assistant 2026.11. Después, sigue los pasos de abajo desde el punto en que IntelliKeep está abierto.

## Marketplace (Home Assistant 2026.11 o posterior)

1. Ve a **Configuración → Marketplace**. La primera vez, lee el aviso y acéptalo
2. Busca **IntelliKeep** y ábrelo
3. Selecciona **Instalar** y, en el diálogo, **Instalar** otra vez
4. Si el Marketplace pide reiniciar, selecciona **Reiniciar Home Assistant**
5. Selecciona **Configurar** y sigue el asistente de configuración. También puedes hacerlo más tarde en **Configuración → Dispositivos y servicios → Añadir integración**

## HACS (versiones anteriores)

1. Abre **HACS** en la barra lateral de Home Assistant
2. Busca **IntelliKeep** y haz clic en **Descargar**
3. **Reinicia Home Assistant**
4. Ve a **Configuración → Dispositivos y servicios → Añadir integración**
5. Busca **IntelliKeep** y sigue el asistente de configuración

Al terminar, el **panel de IntelliKeep** aparece en la barra lateral de Home Assistant, y la [tarjeta del panel de control](../lovelace-card) queda lista para añadirla a cualquier panel de control.

## Actualizar

Con el Marketplace, las versiones nuevas aparecen en **Configuración → Actualizaciones**. Con HACS, aparecen en HACS. Instala la actualización y reinicia Home Assistant. Lee antes el [registro de cambios](https://github.com/henriquekraemer/intellikeep/blob/main/CHANGELOG.md) y, si pasas de la 1.x a la 2.x, lee [Actualizar desde la 1.x](./upgrading).

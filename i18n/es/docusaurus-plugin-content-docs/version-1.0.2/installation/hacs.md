---
sidebar_position: 1
title: Instalar mediante HACS
---

# Instalar mediante HACS

HACS (Home Assistant Community Store) es el método de instalación recomendado.

## Requisitos previos

- [HACS](https://hacs.xyz) instalado en tu instancia de Home Assistant
- Home Assistant 2024.1 o superior

## Pasos

1. Abre **HACS** en la barra lateral de Home Assistant
2. Ve a **Integraciones**
3. Haz clic en el menú de tres puntos (⋮) → **Repositorios personalizados**
4. Agrega la URL del repositorio:
   ```
   https://github.com/intellilar/intellikeep
   ```
   Selecciona **Integración** como categoría y haz clic en **Agregar**
5. Busca **IntelliKeep** en la lista de Integraciones de HACS y haz clic en **Descargar**
6. **Reinicia Home Assistant**
7. Ve a **Configuración → Dispositivos y Servicios → Agregar Integración**
8. Busca **IntelliKeep** y sigue el asistente de configuración

Tras la configuración, el **panel IntelliKeep** aparecerá automáticamente en la barra lateral de Home Assistant.

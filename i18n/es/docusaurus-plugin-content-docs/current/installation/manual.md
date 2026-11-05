---
sidebar_position: 2
title: Instalación manual
---

# Instalación manual

Usa la instalación manual si prefieres no usar HACS ni el Marketplace.

## Pasos

1. Descarga o clona el [repositorio de IntelliKeep](https://github.com/henriquekraemer/intellikeep)
2. Copia el directorio `custom_components/intellikeep/` en el directorio de configuración de Home Assistant:
   ```
   config/custom_components/intellikeep/
   ```
3. **Reinicia Home Assistant**
4. Ve a **Configuración → Dispositivos y servicios → Añadir integración**
5. Busca **IntelliKeep** y sigue el asistente de configuración

## Estructura de directorios

Después de copiarlo, tu directorio de configuración debería contener:

```
config/
└── custom_components/
    └── intellikeep/
        ├── __init__.py
        ├── manifest.json
        ├── brand/
        │   ├── icon.png
        │   ├── logo.png
        │   └── ...
        ├── frontend/
        │   ├── intellikeep-card.js
        │   ├── intellikeep-icons.js
        │   └── intellikeep-panel.js
        ├── translations/
        └── ...
```

Los paquetes del frontend ya vienen compilados e incluidos en el repositorio, así que no hay nada que compilar.

## Actualizar manualmente

Para actualizar, descarga la última versión, reemplaza todo el directorio `custom_components/intellikeep/` (no solo algunos de sus archivos) y reinicia Home Assistant. Si pasas de la 1.x a la 2.x, lee primero [Actualizar desde la 1.x](./upgrading).

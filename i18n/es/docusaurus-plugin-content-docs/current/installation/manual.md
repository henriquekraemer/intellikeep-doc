---
sidebar_position: 2
title: Instalación Manual
---

# Instalación Manual

Usa la instalación manual si prefieres no usar HACS.

## Pasos

1. Descarga o clona el [repositorio IntelliKeep](https://github.com/intellilar/intellikeep)
2. Copia el directorio `custom_components/intellikeep/` en el directorio de configuración de Home Assistant:
   ```
   config/custom_components/intellikeep/
   ```
3. **Reinicia Home Assistant**
4. Ve a **Configuración → Dispositivos y Servicios → Agregar Integración**
5. Busca **IntelliKeep** y sigue el asistente de configuración

## Estructura de directorios

Tras copiar, el directorio de configuración debe contener:

```
config/
└── custom_components/
    └── intellikeep/
        ├── __init__.py
        ├── manifest.json
        ├── frontend/
        │   ├── intellikeep-card.js
        │   └── intellikeep-panel.js
        └── ...
```

## Actualización manual

Para actualizar, repite los pasos anteriores: descarga la última versión y reemplaza el directorio `custom_components/intellikeep/`, luego reinicia Home Assistant.

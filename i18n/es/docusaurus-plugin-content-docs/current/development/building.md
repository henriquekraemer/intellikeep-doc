---
sidebar_position: 1
title: Compilar el Frontend
---

# Compilar el Frontend

La tarjeta Lovelace y el panel lateral se compilan mediante un script basado en Docker. No se requiere instalación local de Node.js.

## Requisitos previos

- Docker ejecutándose localmente
- El repositorio IntelliKeep clonado

## Compilar todo (tarjeta + panel)

```bash
./build-frontend.sh
```

## Compilar solo la tarjeta o el panel

```bash
./build-frontend.sh card
./build-frontend.sh panel
```

El script usa internamente `node:20-alpine` para ejecutar `npm install` y `rollup` dentro de un contenedor.

## Archivos de salida

Los archivos compilados se escriben en:

```
custom_components/intellikeep/frontend/intellikeep-card.js
custom_components/intellikeep/frontend/intellikeep-panel.js
```

## Despliegue en una instancia de HA basada en Docker

Tras compilar, copia los archivos actualizados al contenedor en ejecución:

```bash
# Copiar toda la integración
docker cp custom_components/intellikeep/ homeassistant:/config/custom_components/

# O copiar solo los archivos de frontend actualizados
docker cp custom_components/intellikeep/frontend/intellikeep-panel.js \
  homeassistant:/config/custom_components/intellikeep/frontend/intellikeep-panel.js

docker restart homeassistant
```

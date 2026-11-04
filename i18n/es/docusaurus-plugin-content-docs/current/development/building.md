---
sidebar_position: 1
title: Compilar el frontend
---

# Compilar el frontend

El panel de la barra lateral y la tarjeta Lovelace son componentes web de Lit escritos en TypeScript y empaquetados con Rollup. Un script basado en Docker los compila, así que no necesitas tener Node.js instalado.

## Requisitos previos

- Docker ejecutándose en local
- El [repositorio de IntelliKeep](https://github.com/henriquekraemer/intellikeep) clonado

## Compilar todo (tarjeta + panel)

```bash
./build-frontend.sh
```

## Compilar solo la tarjeta o el panel

```bash
./build-frontend.sh card
./build-frontend.sh panel
```

El script ejecuta `npm install` y `rollup` dentro de un contenedor `node:20-alpine`.

## Compilar sin Docker

Con Node.js 20 o posterior instalado, puedes compilar cada parte directamente:

```bash
cd panel && npm install && npm run build
cd lovelace-card && npm install && npm run build
```

## Archivos de salida

Los archivos compilados se escriben en:

```
custom_components/intellikeep/frontend/intellikeep-card.js
custom_components/intellikeep/frontend/intellikeep-panel.js
```

Estos paquetes se incluyen en el repositorio porque HACS instala la integración directamente desde él. Después de cualquier cambio en el frontend, vuelve a compilarlos y haz commit de ellos.

## Desplegar en una instancia de HA basada en Docker

Después de compilar, copia los archivos actualizados en el contenedor en ejecución:

```bash
# Copy the entire integration
docker cp custom_components/intellikeep/ homeassistant:/config/custom_components/

# Or copy only an updated frontend file
docker cp custom_components/intellikeep/frontend/intellikeep-panel.js \
  homeassistant:/config/custom_components/intellikeep/frontend/intellikeep-panel.js

docker restart homeassistant
```

## Traducciones

El backend y el frontend tienen traducciones separadas:

- El backend usa `strings.json` y `translations/{en,es,pt}.json` (configuración, opciones, acciones y nombres de entidades)
- El panel tiene su propia tabla en `panel/src/translations.ts`, y la tarjeta, en `lovelace-card/src/translations.ts`

Un cambio en un texto visible para el usuario suele afectar a más de uno de ellos.

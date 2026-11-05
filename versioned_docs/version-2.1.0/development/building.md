---
sidebar_position: 1
title: Building the Frontend
---

# Building the Frontend

The sidebar panel and the Lovelace card are Lit web components written in TypeScript and bundled with Rollup. A Docker-based script builds them, so you don't need Node.js installed.

## Prerequisites

- Docker running locally
- The [IntelliKeep repository](https://github.com/henriquekraemer/intellikeep) cloned

## Build all (card + panel)

```bash
./build-frontend.sh
```

## Build only the card or the panel

```bash
./build-frontend.sh card
./build-frontend.sh panel
```

The script runs `npm install` and `rollup` inside a `node:20-alpine` container.

## Building without Docker

With Node.js 20 or later installed, you can build each part directly:

```bash
cd panel && npm install && npm run build
cd lovelace-card && npm install && npm run build
```

## Output files

Built files are written to:

```
custom_components/intellikeep/frontend/intellikeep-card.js
custom_components/intellikeep/frontend/intellikeep-panel.js
```

These bundles are committed to the repository, because HACS and the Marketplace install the integration straight from it. After any frontend change, rebuild and commit them.

## Deploying to a Docker-based HA instance

After building, copy the updated files into the running container:

```bash
# Copy the entire integration
docker cp custom_components/intellikeep/ homeassistant:/config/custom_components/

# Or copy only an updated frontend file
docker cp custom_components/intellikeep/frontend/intellikeep-panel.js \
  homeassistant:/config/custom_components/intellikeep/frontend/intellikeep-panel.js

docker restart homeassistant
```

## Translations

The backend and the frontend have separate translations:

- The backend uses `strings.json` and `translations/{en,es,pt}.json` (setup, options, actions and entity names)
- The panel has its own table in `panel/src/translations.ts`, and the card in `lovelace-card/src/translations.ts`

A change to user-visible text usually touches more than one of them.

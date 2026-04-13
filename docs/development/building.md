---
sidebar_position: 1
title: Building the Frontend
---

# Building the Frontend

The Lovelace card and sidebar panel are built via a Docker-based script. No local Node.js installation is required.

## Prerequisites

- Docker running locally
- The IntelliKeep repository cloned

## Build all (card + panel)

```bash
./build-frontend.sh
```

## Build only the card or panel

```bash
./build-frontend.sh card
./build-frontend.sh panel
```

The script uses `node:20-alpine` internally to run `npm install` and `rollup` inside a container.

## Output files

Built files are written to:

```
custom_components/intellikeep/frontend/intellikeep-card.js
custom_components/intellikeep/frontend/intellikeep-panel.js
```

## Deploying to a Docker-based HA instance

After building, copy the updated files into the running container:

```bash
# Copy the entire integration
docker cp custom_components/intellikeep/ homeassistant:/config/custom_components/

# Or copy only updated frontend files
docker cp custom_components/intellikeep/frontend/intellikeep-panel.js \
  homeassistant:/config/custom_components/intellikeep/frontend/intellikeep-panel.js

docker restart homeassistant
```

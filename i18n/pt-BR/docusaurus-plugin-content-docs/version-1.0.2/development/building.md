---
sidebar_position: 1
title: Compilando o Frontend
---

# Compilando o Frontend

O cartão Lovelace e o painel lateral são compilados via um script baseado em Docker. Nenhuma instalação local do Node.js é necessária.

## Pré-requisitos

- Docker em execução localmente
- O repositório IntelliKeep clonado

## Compilar tudo (cartão + painel)

```bash
./build-frontend.sh
```

## Compilar apenas o cartão ou o painel

```bash
./build-frontend.sh card
./build-frontend.sh panel
```

O script usa internamente `node:20-alpine` para executar `npm install` e `rollup` dentro de um container.

## Arquivos de saída

Os arquivos compilados são gravados em:

```
custom_components/intellikeep/frontend/intellikeep-card.js
custom_components/intellikeep/frontend/intellikeep-panel.js
```

## Implantando em uma instância HA baseada em Docker

Após compilar, copie os arquivos atualizados para o container em execução:

```bash
# Copiar toda a integração
docker cp custom_components/intellikeep/ homeassistant:/config/custom_components/

# Ou copiar apenas os arquivos de frontend atualizados
docker cp custom_components/intellikeep/frontend/intellikeep-panel.js \
  homeassistant:/config/custom_components/intellikeep/frontend/intellikeep-panel.js

docker restart homeassistant
```

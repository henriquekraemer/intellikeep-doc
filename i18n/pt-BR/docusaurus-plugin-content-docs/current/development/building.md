---
sidebar_position: 1
title: Compilando o Frontend
---

# Compilando o Frontend

O painel da barra lateral e o card Lovelace são web components Lit escritos em TypeScript e empacotados com o Rollup. Um script baseado em Docker faz o build, então você não precisa ter o Node.js instalado.

## Pré-requisitos

- Docker rodando localmente
- O [repositório do IntelliKeep](https://github.com/henriquekraemer/intellikeep) clonado

## Compilar tudo (card + painel)

```bash
./build-frontend.sh
```

## Compilar só o card ou só o painel

```bash
./build-frontend.sh card
./build-frontend.sh panel
```

O script roda `npm install` e `rollup` dentro de um contêiner `node:20-alpine`.

## Compilando sem Docker

Com o Node.js 20 ou mais recente instalado, você pode compilar cada parte diretamente:

```bash
cd panel && npm install && npm run build
cd lovelace-card && npm install && npm run build
```

## Arquivos gerados

Os arquivos compilados são gravados em:

```
custom_components/intellikeep/frontend/intellikeep-card.js
custom_components/intellikeep/frontend/intellikeep-panel.js
```

Esses bundles ficam versionados no repositório, porque o HACS instala a integração direto dele. Depois de qualquer mudança no frontend, compile de novo e faça commit deles.

## Publicando em uma instância do HA baseada em Docker

Depois do build, copie os arquivos atualizados para o contêiner em execução:

```bash
# Copy the entire integration
docker cp custom_components/intellikeep/ homeassistant:/config/custom_components/

# Or copy only an updated frontend file
docker cp custom_components/intellikeep/frontend/intellikeep-panel.js \
  homeassistant:/config/custom_components/intellikeep/frontend/intellikeep-panel.js

docker restart homeassistant
```

## Traduções

O backend e o frontend têm traduções separadas:

- O backend usa `strings.json` e `translations/{en,es,pt}.json` (configuração, opções, ações e nomes de entidades)
- O painel tem a própria tabela em `panel/src/translations.ts`, e o card, em `lovelace-card/src/translations.ts`

Uma mudança em um texto visível para o usuário costuma mexer em mais de um deles.

---
sidebar_position: 1
title: Instalar via HACS
---

# Instalar via HACS

O HACS (Home Assistant Community Store) é a forma de instalação recomendada. Ele também avisa você quando sai uma nova versão.

## Pré-requisitos

- [HACS](https://hacs.xyz) instalado na sua instância do Home Assistant
- Home Assistant 2026.1 ou mais recente

## Passo a passo

1. Abra o **HACS** na barra lateral do Home Assistant
2. Clique no menu de três pontos (⋮) no canto superior direito → **Repositórios personalizados**
3. Adicione a URL do repositório:
   ```
   https://github.com/henriquekraemer/intellikeep
   ```
   Escolha **Integração** como tipo e clique em **Adicionar**
4. Procure por **IntelliKeep** no HACS e clique em **Baixar**
5. **Reinicie o Home Assistant**
6. Vá em **Configurações → Dispositivos & serviços → Adicionar integração**
7. Procure por **IntelliKeep** e siga o assistente de configuração

Depois da configuração, o **painel do IntelliKeep** aparece na barra lateral do Home Assistant, e o [card de dashboard](../lovelace-card) já pode ser adicionado a qualquer dashboard.

## Atualizando

Quando o HACS mostrar uma atualização do IntelliKeep, baixe-a e reinicie o Home Assistant. Leia antes o [changelog](https://github.com/henriquekraemer/intellikeep/blob/main/CHANGELOG.md) e, se estiver passando da 1.x para a 2.x, leia [Atualizando da 1.x](./upgrading).

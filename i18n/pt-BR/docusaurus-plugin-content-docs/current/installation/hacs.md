---
sidebar_position: 1
title: Instalar via HACS ou Marketplace
---

# Instalar via HACS ou Marketplace

O IntelliKeep está na lista padrão do HACS, então você o encontra pela busca, sem adicionar um repositório personalizado. O Home Assistant 2026.11 e mais recentes trazem o **Marketplace**, que instala a partir do mesmo catálogo. Em versões anteriores, use o [HACS](https://hacs.xyz). Qualquer um dos dois é a forma de instalação recomendada, e os dois avisam você quando sai uma nova versão.

## Pré-requisitos

- Home Assistant 2026.1 ou mais recente
- Antes do Home Assistant 2026.11, o [HACS](https://hacs.xyz) instalado na sua instância do Home Assistant

## Abrir o IntelliKeep direto

[![Abrir o IntelliKeep no Marketplace da sua instância do Home Assistant.](https://my.home-assistant.io/badges/marketplace_repository.svg)](https://my.home-assistant.io/redirect/marketplace_repository/?owner=henriquekraemer&repository=intellikeep&category=integration)

O botão abre o IntelliKeep no Marketplace, ou no HACS antes do Home Assistant 2026.11. Depois, siga os passos abaixo a partir do ponto em que o IntelliKeep está aberto.

## Marketplace (Home Assistant 2026.11 ou mais recente)

1. Vá em **Configurações → Marketplace**. Na primeira vez, leia o aviso e aceite-o
2. Procure por **IntelliKeep** e abra-o
3. Selecione **Instalar** e, na janela que abrir, **Instalar** de novo
4. Se o Marketplace pedir para reiniciar, selecione **Reiniciar o Home Assistant**
5. Selecione **Definir** e siga o assistente de configuração. Você também pode fazer isso depois em **Configurações → Dispositivos & serviços → Adicionar integração**

## HACS (versões anteriores)

1. Abra o **HACS** na barra lateral do Home Assistant
2. Procure por **IntelliKeep** e clique em **Baixar**
3. **Reinicie o Home Assistant**
4. Vá em **Configurações → Dispositivos & serviços → Adicionar integração**
5. Procure por **IntelliKeep** e siga o assistente de configuração

Depois da configuração, o **painel do IntelliKeep** aparece na barra lateral do Home Assistant, e o [card de dashboard](../lovelace-card) já pode ser adicionado a qualquer dashboard.

## Atualizando

Com o Marketplace, as novas versões aparecem em **Configurações → Atualizações**. Com o HACS, elas aparecem no próprio HACS. Instale a atualização e reinicie o Home Assistant. Leia antes o [changelog](https://github.com/henriquekraemer/intellikeep/blob/main/CHANGELOG.md) e, se estiver passando da 1.x para a 2.x, leia [Atualizando da 1.x](./upgrading).

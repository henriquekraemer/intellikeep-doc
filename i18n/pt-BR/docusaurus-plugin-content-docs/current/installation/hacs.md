---
sidebar_position: 1
title: Instalar via HACS
---

# Instalar via HACS

O HACS (Home Assistant Community Store) é o método de instalação recomendado.

## Pré-requisitos

- [HACS](https://hacs.xyz) instalado na sua instância do Home Assistant
- Home Assistant 2024.1 ou superior

## Passos

1. Abra o **HACS** na barra lateral do Home Assistant
2. Vá em **Integrações**
3. Clique no menu de três pontos (⋮) → **Repositórios personalizados**
4. Adicione a URL do repositório:
   ```
   https://github.com/intellilar/intellikeep
   ```
   Selecione **Integração** como categoria e clique em **Adicionar**
5. Pesquise por **IntelliKeep** na lista de Integrações do HACS e clique em **Baixar**
6. **Reinicie o Home Assistant**
7. Vá em **Configurações → Dispositivos e Serviços → Adicionar Integração**
8. Pesquise por **IntelliKeep** e siga o assistente de configuração

Após a configuração, o **painel IntelliKeep** aparecerá automaticamente na barra lateral do Home Assistant.

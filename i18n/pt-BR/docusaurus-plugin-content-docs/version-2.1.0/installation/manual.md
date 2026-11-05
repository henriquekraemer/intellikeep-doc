---
sidebar_position: 2
title: Instalação Manual
---

# Instalação Manual

Use a instalação manual se preferir não usar o HACS nem o Marketplace.

## Passo a passo

1. Baixe ou clone o [repositório do IntelliKeep](https://github.com/henriquekraemer/intellikeep)
2. Copie a pasta `custom_components/intellikeep/` para a pasta de configuração do Home Assistant:
   ```
   config/custom_components/intellikeep/
   ```
3. **Reinicie o Home Assistant**
4. Vá em **Configurações → Dispositivos & serviços → Adicionar integração**
5. Procure por **IntelliKeep** e siga o assistente de configuração

## Estrutura de pastas

Depois de copiar, a sua pasta de configuração deve ter:

```
config/
└── custom_components/
    └── intellikeep/
        ├── __init__.py
        ├── manifest.json
        ├── brand/
        │   ├── icon.png
        │   ├── logo.png
        │   └── ...
        ├── frontend/
        │   ├── intellikeep-card.js
        │   ├── intellikeep-icons.js
        │   └── intellikeep-panel.js
        ├── translations/
        └── ...
```

Os bundles do frontend já vêm compilados e incluídos no repositório, então não há nada para compilar.

## Atualizando manualmente

Para atualizar, baixe a versão mais recente, substitua a pasta `custom_components/intellikeep/` inteira (e não só alguns arquivos dela) e reinicie o Home Assistant. Se estiver passando da 1.x para a 2.x, leia antes [Atualizando da 1.x](./upgrading).

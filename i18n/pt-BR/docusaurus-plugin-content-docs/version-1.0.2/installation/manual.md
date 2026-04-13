---
sidebar_position: 2
title: Instalação Manual
---

# Instalação Manual

Use a instalação manual se preferir não usar o HACS.

## Passos

1. Baixe ou clone o [repositório IntelliKeep](https://github.com/intellilar/intellikeep)
2. Copie o diretório `custom_components/intellikeep/` para o diretório de configuração do Home Assistant:
   ```
   config/custom_components/intellikeep/
   ```
3. **Reinicie o Home Assistant**
4. Vá em **Configurações → Dispositivos e Serviços → Adicionar Integração**
5. Pesquise por **IntelliKeep** e siga o assistente de configuração

## Estrutura de diretórios

Após a cópia, o diretório de configuração deve conter:

```
config/
└── custom_components/
    └── intellikeep/
        ├── __init__.py
        ├── manifest.json
        ├── frontend/
        │   ├── intellikeep-card.js
        │   └── intellikeep-panel.js
        └── ...
```

## Atualizando manualmente

Para atualizar, repita os passos acima: baixe o release mais recente e substitua o diretório `custom_components/intellikeep/`, depois reinicie o Home Assistant.

---
sidebar_position: 2
title: Manual Installation
---

# Manual Installation

Use manual installation if you prefer not to use HACS.

## Steps

1. Download or clone the [IntelliKeep repository](https://github.com/intellilar/intellikeep)
2. Copy the `custom_components/intellikeep/` directory into your Home Assistant config directory:
   ```
   config/custom_components/intellikeep/
   ```
3. **Restart Home Assistant**
4. Go to **Settings → Devices & Services → Add Integration**
5. Search for **IntelliKeep** and follow the setup wizard

## Directory structure

After copying, your config directory should contain:

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

## Updating manually

To update, repeat the steps above: download the latest release and overwrite the `custom_components/intellikeep/` directory, then restart Home Assistant.

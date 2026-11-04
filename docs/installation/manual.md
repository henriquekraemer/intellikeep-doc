---
sidebar_position: 2
title: Manual Installation
---

# Manual Installation

Use manual installation if you prefer not to use HACS.

## Steps

1. Download or clone the [IntelliKeep repository](https://github.com/henriquekraemer/intellikeep)
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

The frontend bundles are already built and included in the repository, so there is nothing to compile.

## Updating manually

To update, download the latest release, replace the whole `custom_components/intellikeep/` directory (not just some of its files), and restart Home Assistant. If you are moving from 1.x to 2.x, read [Upgrading from 1.x](./upgrading) first.

---
sidebar_position: 1
title: Install via HACS
---

# Install via HACS

HACS (Home Assistant Community Store) is the recommended installation method. It also tells you when a new version is out.

## Prerequisites

- [HACS](https://hacs.xyz) installed in your Home Assistant instance
- Home Assistant 2026.1 or later

## Steps

1. Open **HACS** in your Home Assistant sidebar
2. Click the three-dot menu (⋮) in the top right corner → **Custom repositories**
3. Add the repository URL:
   ```
   https://github.com/henriquekraemer/intellikeep
   ```
   Select **Integration** as the type and click **Add**
4. Search for **IntelliKeep** in HACS and click **Download**
5. **Restart Home Assistant**
6. Go to **Settings → Devices & Services → Add Integration**
7. Search for **IntelliKeep** and follow the setup wizard

After setup, the **IntelliKeep panel** shows up in the Home Assistant sidebar, and the [dashboard card](../lovelace-card) is ready to be added to any dashboard.

## Updating

When HACS shows an update for IntelliKeep, download it and restart Home Assistant. Read the [changelog](https://github.com/henriquekraemer/intellikeep/blob/main/CHANGELOG.md) first, and if you are moving from 1.x to 2.x, read [Upgrading from 1.x](./upgrading).

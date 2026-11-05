---
sidebar_position: 1
title: Install via HACS or the Marketplace
---

# Install via HACS or the Marketplace

IntelliKeep is in the HACS default list, so you can find it with a search, without adding a custom repository. Home Assistant 2026.11 and later include the **Marketplace**, which installs from the same catalog. On earlier versions, use [HACS](https://hacs.xyz). Either one is the recommended installation method, and both tell you when a new version is out.

## Prerequisites

- Home Assistant 2026.1 or later
- Before Home Assistant 2026.11, [HACS](https://hacs.xyz) installed in your Home Assistant instance

## Open IntelliKeep directly

[![Open IntelliKeep in the Marketplace of your Home Assistant instance.](https://my.home-assistant.io/badges/marketplace_repository.svg)](https://my.home-assistant.io/redirect/marketplace_repository/?owner=henriquekraemer&repository=intellikeep&category=integration)

The button opens IntelliKeep in the Marketplace, or in HACS before Home Assistant 2026.11. Then follow the steps below from the point where IntelliKeep is open.

## Marketplace (Home Assistant 2026.11 or later)

1. Go to **Settings → Marketplace**. The first time, read the warning and accept it
2. Search for **IntelliKeep** and open it
3. Select **Install**, then **Install** again in the dialog
4. If the Marketplace asks for a restart, select **Restart Home Assistant**
5. Select **Set up** and follow the setup wizard. You can also do it later under **Settings → Devices & Services → Add Integration**

## HACS (earlier versions)

1. Open **HACS** in your Home Assistant sidebar
2. Search for **IntelliKeep** and click **Download**
3. **Restart Home Assistant**
4. Go to **Settings → Devices & Services → Add Integration**
5. Search for **IntelliKeep** and follow the setup wizard

After setup, the **IntelliKeep panel** shows up in the Home Assistant sidebar, and the [dashboard card](../lovelace-card) is ready to be added to any dashboard.

## Updating

With the Marketplace, new versions show up under **Settings → Updates**. With HACS, they show up in HACS. Install the update and restart Home Assistant. Read the [changelog](https://github.com/henriquekraemer/intellikeep/blob/main/CHANGELOG.md) first, and if you are moving from 1.x to 2.x, read [Upgrading from 1.x](./upgrading).

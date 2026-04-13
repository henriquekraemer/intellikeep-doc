---
sidebar_position: 1
title: Install via HACS
---

# Install via HACS

HACS (Home Assistant Community Store) is the recommended installation method.

## Prerequisites

- [HACS](https://hacs.xyz) installed in your Home Assistant instance
- Home Assistant 2024.1 or later

## Steps

1. Open **HACS** in your Home Assistant sidebar
2. Go to **Integrations**
3. Click the three-dot menu (⋮) → **Custom repositories**
4. Add the repository URL:
   ```
   https://github.com/intellilar/intellikeep
   ```
   Select **Integration** as the category and click **Add**
5. Search for **IntelliKeep** in the HACS Integrations list and click **Download**
6. **Restart Home Assistant**
7. Go to **Settings → Devices & Services → Add Integration**
8. Search for **IntelliKeep** and follow the setup wizard

After setup, the **IntelliKeep panel** will appear automatically in the Home Assistant sidebar.

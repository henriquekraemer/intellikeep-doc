---
sidebar_position: 3
title: Configuration
---

# Configuration

## Initial setup

During the integration setup wizard you can configure:

| Option | Default | Description |
|---|---|---|
| **Instance Name** | `IntelliKeep` | Label shown in Home Assistant |
| **Notify Days Before** | `1` | Days before a task's due date to send a reminder |
| **Notification Service** | *(empty)* | Optional `notify.*` service, e.g. `notify.mobile_app_my_phone` |

## Changing settings later

All options can be updated after installation:

1. Go to **Settings → Devices & Services**
2. Find the **IntelliKeep** entry
3. Click **Configure** to adjust settings, or **Reconfigure** to run the setup wizard again

## Notification service

Leave **Notification Service** empty to use only Home Assistant persistent notifications (the bell icon in the HA UI).

To also receive mobile push notifications, enter a `notify.*` service name. You can find available services in **Developer Tools → Actions**.

Example values:
- `notify.mobile_app_my_phone`
- `notify.all_devices`

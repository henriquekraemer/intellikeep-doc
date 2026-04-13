---
sidebar_position: 1
title: Tasks
---

# Tasks

The Tasks view is the main panel in IntelliKeep. It shows all pending and completed tasks with powerful filtering and search.

## Creating a task

Tasks can be created from the panel UI or via the [`intellikeep.create_task`](../services#intellikeepcreate_task) service action.

### Task fields

| Field | Description |
|---|---|
| **Name** | Task title |
| **Priority** | `low`, `medium`, `high`, or `critical` |
| **Due date** | When the task is due |
| **Frequency** | Recurrence: `once`, `daily`, `weekly`, `monthly`, `yearly`, or a custom interval in days |
| **Linked entities** | HA areas or specific device IDs |
| **Notify days before** | Override the global notification lead time for this task |
| **Description** | Optional free-text description |

## Recurring tasks

When a recurring task is completed, a new instance is automatically created with the next due date calculated from the frequency setting.

Supported frequencies:
- `once` — no recurrence
- `daily`
- `weekly`
- `monthly`
- `yearly`
- Custom interval (specify a number of days)

## Priority levels

Priorities are displayed as a color-coded bar on each task card:

| Priority | Color |
|---|---|
| Low | Green |
| Medium | Yellow |
| High | Orange |
| Critical | Red |

## Filtering and search

The Tasks view supports filtering by:
- **Area** — show tasks linked to a specific HA area
- **Device** — show tasks linked to a specific device
- **Priority** — filter by one or more priority levels
- **Free-text search** — filter by task name

## Notes

Each task has a dedicated Notes section. Notes are timestamped and record the author (HA user who added them). Notes can be added, viewed, and deleted from the task detail view.

## Activity log

Every change to a task is recorded in its Activity Log:
- Task created
- Fields edited
- Task completed (with completion timestamp)
- Task reopened
- Notes added or deleted

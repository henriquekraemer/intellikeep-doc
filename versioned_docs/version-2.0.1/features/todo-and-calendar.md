---
sidebar_position: 4
title: To-do List & Calendar
---

# To-do List & Calendar

IntelliKeep adds two entities that put your tasks in Home Assistant's own **To-do lists** and **Calendar**, so you can see and complete them outside the IntelliKeep panel, use them in other cards, and build automations on them.

## To-do list

**`todo.intellikeep_tasks`** shows the open tasks by due date in Home Assistant's To-do lists, followed by the tasks completed in the last 30 days.

- **Checking** an item completes the task, and a recurring task gets its next occurrence. **Unchecking** it reopens the task and removes that occurrence, like **Undo** in the panel.
- The task history records the Home Assistant user who checked or unchecked the item.
- Items **added** to the list become one-time tasks. Their name, description and due date can be edited from the list.
- **Deleting** an open item deletes the task. Completed tasks keep their history, so they can't be deleted here, and **Clear completed** is refused. They leave the list 30 days after completion, or you can delete them in the panel.
- The `todo.*` actions work too, for example `todo.add_item` from a voice assistant or an automation:

```yaml
action: todo.add_item
target:
  entity_id: todo.intellikeep_tasks
data:
  item: Replace the doorbell battery
  due_date: "2026-12-01"
```

Tasks created this way are one-time tasks with the default priority. Open them in the panel to set a priority, an icon or a repeat.

## Calendar

**`calendar.intellikeep_tasks`** shows each open task on its due date, overdue ones included. It appears in Home Assistant's **Calendar** and can be used in calendar cards.

- A task with a due time is an event at that time. A task due at midnight (no time set) is an all-day event.
- Completed tasks are left out, so a task done early doesn't trigger automations at its old due time.
- Future repeats are not projected: the next occurrence shows up once the current one is completed, so calendar triggers fire only for real tasks. The panel's [Calendar tab](./calendar#future-repeats) does show the future repeats.
- The calendar is read-only. Create and edit tasks in the panel or in the to-do list.

The entity's state is `on` while an all-day task is due today, and its attributes describe the task due today or next.

### Calendar triggers

Use a calendar trigger to act when a task becomes due:

```yaml
automation:
  alias: Remind me when a maintenance task is due
  triggers:
    - trigger: calendar
      event: start
      entity_id: calendar.intellikeep_tasks
  actions:
    - action: notify.mobile_app_my_phone
      data:
        title: Maintenance due
        message: "{{ trigger.calendar_event.summary }}"
```

All-day tasks start at local midnight. The trigger's `offset` moves the trigger time for every task, for example `offset: "-01:00:00"` fires one hour before each task is due.

More examples are in [Automations](../automations).

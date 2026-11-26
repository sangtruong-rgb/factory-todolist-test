# Todolist

> Confirmed by the owner on 2026-11-26 during factory-init. Changes after this go through an issue, not an edit here.

## Problem

A person wants a quick place to keep the tasks of their day, without an account, that is still there when they come back. This project is also a test of the Factory pipeline (ba-ticket, factory-init, factory).

## Success

The four tickets #1 to #4 are built by factory runs and each passes its criteria and its QC.

## Users

| User | What they do here | How often, on what device | Must never see |
|---|---|---|---|
| A person planning their day | Add, tick, edit, delete, filter tasks; give them due dates | Several times a day, desktop and phone browser | Another person's tasks (tasks never leave the browser) |

## MVP

A person can keep a list of tasks in their browser, tick them off, edit them, filter them and see which are overdue.

### Journeys

1. **Keep a list** (person): open the page → add a task → tick it when done → delete it. An empty title is refused with a message; tasks survive a reload. (#1)
2. **Fix a task** (person): press the pencil → change the title → Save, or Cancel / Escape. An empty title is refused. (#2)
3. **Focus** (person): see how many are left → filter Active / Done → Clear completed. (#3)
4. **Deadlines** (person): add a task with a due date → see "Today" or "Overdue, 25 Nov" → change or remove the date in edit mode. (#4)

### Rules

In the criteria of #1 to #4 and in `.factory/decisions.md`.

### Numbers

One person per browser; tens to a few hundred tasks; a title is at most 200 characters.

## Later

- Accounts and sync between devices: not asked for.
- Reordering, undo, search, sorting, reminders, recurring tasks: not asked for.

## Constraints

No server and no sign-in: tasks stay in the browser. English UI. Light and dark follow the system. No animation.

## References

The agreed look is the prototype of #1 (`prototype/issue-1`): "Calm & spare", one green accent, system fonts.

## Open

None.

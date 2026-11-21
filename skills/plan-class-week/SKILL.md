---
name: plan-class-week
description: Plan and publish a week of classes, or create and change a repeating class timetable, at a Fabslots studio, gym, dance school, swim school or other class business. Use for "copy last week's classes", "add a Saturday class", "new term timetable", "change who teaches Thursday", "cancel Tuesday's class" and "stop the evening class from January".
---

# Plan the class week

There are two ways to change classes. Changing the **repeating timetable** affects every week from a date. **Planning
one week** with `plan_week` changes only that week. If it isn't clear whether the owner means every week or just one,
ask. Call `list_sessions` first to see what is already scheduled and booked.

Get class IDs from `list_services` and instructor IDs from `list_team`. Don't guess them.

## Repeating timetable

| owner says | tool |
|---|---|
| "Add Yoga every Mon and Wed at 18:00" | `create_timetable`: weekdays, time, instructor, capacity, start and optional end date. The preview lists the sessions it will create; confirm after the owner's yes. |
| "One extra class this Saturday" | `add_session` with the local date and time |
| "Change Thursday's instructor / capacity / time" | `update_session` for that one session |
| "Cancel Tuesday's class" | `cancel_session`. The preview shows who is booked, emailed and refunded credits; confirm after yes. |
| "Stop the evening class from January" | `end_timetable` from that date. The preview lists the sessions and bookings affected. |

## Week-by-week planning

Use `plan_week` with `weekStart` (the first day of the week, using the location's week start):

1. Choose a starting point with `from`: `live` (the week as it is), `week` with `sourceWeek` (copy another week),
   `regular` (the usual timetable) or `empty`.
2. To change the classes, pass `classes` as the **complete** list for the week, with `serviceId`, local `date` and
   `time`, plus `durationMinutes`, `capacity` and `staffIds` where they differ from the class defaults.
3. The first call returns a preview with any conflicts (an instructor booked twice, a class with bookings being
   removed). Show it, fix the conflicts with the owner, then call again with `confirm`.
4. `notifyCustomers` defaults to true: customers with bookings hear about changes. Tell the owner, and pass `false`
   only if they ask.

## Afterwards

Call `list_sessions` for the week and show the final timetable by day, with booked places against capacity.

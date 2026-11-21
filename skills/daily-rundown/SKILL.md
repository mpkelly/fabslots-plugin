---
name: daily-rundown
description: Give a Fabslots owner or staff member a clear rundown of a day or week at their business, covering who is booked and when, free gaps, booking requests waiting for an answer, and classes that are full or nearly full. Use for "what's on today", "what's on tomorrow", "my schedule this week", "who's coming in" and morning briefings.
---

# Daily rundown

## Gather

1. Call `list_businesses` (if you haven't already) for the location and its `today`.
2. Call `get_day_sheet` with the local `date`. For "this week" or "the next few days", pass `days` (up to 7).
3. Call `find_bookings` with `status: "requested"` to find booking requests waiting for approval.
4. For class, tour or timed-entry businesses, call `list_sessions` for the same dates to get booked places, capacity
   and waitlists.

Skip calls that don't fit the business. A salon has no sessions, and a business without request-to-book has no
requests.

## Present

Keep it short enough to read on a phone:

1. **One line first**: "Tomorrow, Thu 20 Nov: 9 bookings, first at 09:00, last ends 18:30."
2. **The day, in time order**, grouped the way the business works: by staff member for appointments, by class for
   studios, by table or area for restaurants, by item for rentals. Show the time, the customer's name and the service.
   Mark anyone new, a big party, or an unpaid booking where the result shows it.
3. **Gaps**: free stretches of an hour or more during opening hours.
4. **Needs you**: requests waiting for an answer, classes at or near capacity, waitlists, unpaid bookings.

When a staff member asks, show only their own schedule unless they ask for everyone.

## Offer the next step

End with one or two useful actions, not a menu. For example: "Approve Ana's request for Saturday?" or "Want me to
move Sam to the 14:00 gap?" Use `respond_to_request` for requests (the customer is emailed either way, so show the
preview first) and the `change-the-schedule` skill for moves.

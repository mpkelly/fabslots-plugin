---
name: change-the-schedule
description: Move, cancel or work around Fabslots bookings when plans change, such as a customer wanting another time, a staff member off sick or on holiday, the business closing for a day, or a class being cancelled. Use for rescheduling, cancelling, adding time off, closing dates and handling the bookings that clash.
---

# Change the schedule

Every change here can email customers. Find the right booking first, show what will happen, and tell the owner
afterwards who was emailed.

## Move a booking

1. Find it with `find_bookings` (customer name, date, or both). If several match, ask which, using time and service.
2. Call `check_availability` for the same service near the time the customer wants. Keep the same staff member
   unless the owner says otherwise.
3. Offer two or three options in local time. If there's nothing, say why (from the result) and offer the next free
   days it returns.
4. Call `reschedule_booking` with the chosen `slotId`. When the customer will be emailed it previews first: show the
   preview and confirm after the owner's yes.
5. Report the new time and whether the customer was emailed.

## Cancel a booking

1. Find it as above.
2. Call `cancel_booking` with the reason if the owner gave one. Show the preview: who is emailed, and any refund or
   returned pass credit.
3. Confirm only after the owner says yes.

Never cancel bookings in bulk on a vague request like "cancel everything next month". Ask which bookings, then handle
them with previews.

## Staff time off or sickness

1. Call `add_time_off` for the person and dates. If bookings or classes clash, the result lists them and asks for
   confirmation.
2. Tell the owner about each clash, then ask what to do with each one:
   - **move** it to someone else or another time (`check_availability`, then `reschedule_booking`)
   - **cancel** it (`cancel_booking`, with its own preview)
   - **keep** it (someone covers)
3. Deal with the clashes first, then confirm the time off.

Staff can add time off for themselves. Only managers and owners can add it for colleagues.

## Close the business, a room, a table area or a resource for a day

Call `close_dates` with `action: "close"`, the date, and a `zone` or `resource` if only part of the business closes.
It previews the confirmed bookings that would be affected; handle them as for time off, then confirm. To reopen,
call `close_dates` with `action: "reopen"` and the `closureId`.

## Cancel a class

Call `cancel_session`. The preview says how many people are booked, who gets an email and which pass credits come
back. Confirm after the owner's yes. For a change of instructor, time or capacity, use `update_session` instead of
cancelling.

## Booking requests

For businesses that approve bookings, `respond_to_request` approves or declines one. The customer is emailed either
way, so show the preview and get the owner's answer first.

## Afterwards

Summarise in one short list: what moved where, what was cancelled, and who was emailed. If anything failed, say which
item and why.

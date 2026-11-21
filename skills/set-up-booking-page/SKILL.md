---
name: set-up-booking-page
description: Set up a new Fabslots online booking page from a conversation, for a salon, studio, gym, clinic, restaurant, rental shop, tour or any booking business, and give the owner a private link to preview, sign up and launch it. Use when someone wants to start taking online bookings, make a booking page, or add a new business or location to Fabslots.
---

# Set up a booking page from a chat

The setup tools work without a Fabslots account. The owner gets a private link, sees their booking page, then signs
up (or in) and launches. Nothing is public until they launch.

## 1. Ask once, then build

Collect what you need in a single round of questions. Don't interview the owner field by field:

- Business name, type and city (the city gives the timezone; infer the currency and language from it)
- What customers book:
  - appointments: services with duration and price, and who does them
  - classes: class types with weekly days and times, instructor and capacity
  - tables, rooms or equipment: what can be booked, how many, for how long
  - rentals or timed entry: items or ticket types, prices and hours
- Who works there (first names are enough) and the opening hours

If the owner already gave most of this, skip the questions and build. Fill gaps with sensible defaults, then list
each assumption so they can correct it: "I've assumed 45 minutes and $40 for a haircut. Change either?" Don't
present an invented price or opening hour as theirs.

## 2. Learn the document format

Call `get_setup_options` with `businessType` set to an exact ID from its `businessTypes` list (for example
`yoga_studio`). If you're not sure which type fits, call it without `businessType` first to see the list.

Follow what it returns: the sections for that type, the `minimalExample`, and the constraints (prices as decimal
strings like `"45.00"`, weekdays `mon` to `sun`, 24-hour `HH:MM` times, and section keys to cross-reference services,
staff, zones and rentals).

## 3. Create the draft

Call `create_setup_draft` with the whole setup document as a JSON object in its `setup` argument (not a string). It
validates everything at once:

- **Errors**: fix every one listed, then call again. Don't fix one per attempt.
- **Warnings**: mention the ones the owner would care about.

## 4. Hand over the link

Give the owner the `claimUrl` and explain it in one or two sentences: it opens a private preview of their booking
page, where they sign up or sign in and press **Launch**. It expires in 14 days. Treat the link and `draftId` as
private: share them only with the owner.

## 5. Make changes

When the owner asks for changes, call `update_setup_draft` with the `draftId`, the last `revision` you received and
the **whole** updated document. If it reports a revision conflict, merge your change into the current document it
returns and try again. The same link shows the new version.

## 6. Launch (only when the owner is connected with an account)

If the user's Fabslots account is connected, you can launch for them:

1. Call `launch_setup_draft` with the `draftId`. To add the setup as a new location of a business they already own,
   pass that business's ID from `list_businesses` as `asLocationOf`.
2. Show the preview and wait for the owner's yes, then call again with `confirm`.
3. Share the `bookingUrl` and `adminUrl` from the result.

If they aren't connected, the link is how they launch; don't ask them to connect just for this.

## After launch

Call `get_location_overview` and mention the top two or three `gaps` it lists (for example, photos or online
payments), with the tool or admin link that fixes each.

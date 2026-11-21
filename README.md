# Fabslots

Set up online bookings for your business from an AI assistant, then run them there. Describe your business and get a
complete booking page (services, team, hours, classes, tables or rentals) with a private link to preview, sign up and
launch; no account is needed until you launch. Then ask what's on tomorrow, move or cancel a booking, give a team
member time off and sort out the bookings that clash, plan next week's classes, or see how the month went in
[Fabslots](https://fabslots.app).

Fabslots handles appointments, classes, restaurant tables, rentals and timed entry, for salons, clinics, gyms, dance
and yoga studios, bike and equipment rentals, cafés, restaurants, tours and other booking businesses.

## What's inside

- **The Fabslots connector** (`https://fabslots.app/mcp`): Fabslots' own remote MCP server, with 51 tools for
  bookings, availability, customers, services, team hours, time off, closures, classes, timetables, passes, gift
  cards, courses, waitlists, reviews, stats and setup.
- **Six skills** that teach the assistant how to use it well:

| skill | for |
|---|---|
| `fabslots-basics` | Ground rules: picking the location, local times, previews before anything that emails a customer, handling errors |
| `set-up-booking-page` | Building a new booking page from one conversation and handing over the launch link |
| `daily-rundown` | "What's on today?": the day by person, class or table, gaps, and requests waiting for an answer |
| `change-the-schedule` | Moving and cancelling bookings, time off, closures and the bookings they clash with |
| `weekly-review` | Stats against the previous period, quiet times, and lapsed customers to win back |
| `plan-class-week` | Repeating timetables and week-by-week class planning |

## Getting started

1. Add the plugin. When the assistant first uses a Fabslots tool, sign in to Fabslots (choose **Sign in now** or
   **Sign in when needed** if your assistant asks).
2. On the Fabslots consent page, pick the businesses to share and choose **Manage** or **View only**.
3. Ask something like "What's on tomorrow?" or "Set me up a booking page for my yoga studio in Lisbon."

You can see and disconnect connected assistants any time under **Connected apps** in the Fabslots admin.
Full guide: [Run bookings from ChatGPT or Claude](https://fabslots.app/guides/run-bookings-from-chatgpt-claude).

## What it sends and stores

- The plugin contains only instructions (the skills) and the connector address. It runs no scripts or hooks.
- Tool calls go to `https://fabslots.app/mcp` only, over HTTPS, signed in with OAuth. Your Fabslots role still
  applies: staff see and change what they can in the admin, and View only connections can't change anything.
- Fabslots keeps an activity log of each assistant action (tool, result, time, and a short summary for changes) for
  90 days, visible to the owner. What your assistant keeps from the conversation is up to its provider.
- Setup tools work without signing in. A setup draft is stored privately for 14 days until you launch it.

## Safety

- Anything that emails a customer or changes many things at once shows a preview first and waits for your yes.
- The assistant can't message customers in bulk, permanently delete data, charge a card or refund one. When it
  cancels a booking that was paid online, the payment waits under "Refunds to review" in the Fabslots admin, where you
  refund it or keep it.
- Billing, payment setup, custom domains, photos and team invites stay in the Fabslots admin. The assistant gives you
  a link.

## Support

Email [support@fabslots.app](mailto:support@fabslots.app) or see [fabslots.app/support](https://fabslots.app/support).
Setup help is in the [guide](https://fabslots.app/guides/run-bookings-from-chatgpt-claude).

[Privacy policy](https://fabslots.app/privacy) · [Terms](https://fabslots.app/terms) · MIT licensed

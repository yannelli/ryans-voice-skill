# PRD

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- Constraints appear once, at the top.
- R1 to R6 are numbered and testable, each with a number or a named control: "R3: ... within 60 seconds."
- Non-goals are flat one-line statements.
- Open questions carry an owner and a date, and "currently unknown" and "TBD" stay as written.
- Metrics pair a baseline with a target.
- The timeline puts one task per line under period labels.

## Waitlist PRD

```text
PRD: Waitlist for Full Time Slots

Constraints: Built on the current booking API (v3). No new SMS vendor. Live before 11/15/2026 for the holiday season.

Problem
When a time slot is full, customers leave the booking page. 31% of booking page visits in August ended on a full slot, and 88% of those visitors did not book another slot that day.

Owners also lose cancelled slots. A cancellation less than 24 hours out is refilled 6% of the time today.

Who it's for
- Customers trying to book a full slot
- Business owners who get cancellations and cannot refill them in time

Requirements
R1: A full slot shows a "Join Waitlist" button in place of "Book".
R2: Joining requires a name and phone number only.
R3: When a booking in that slot is cancelled, the first person on the waitlist gets a text within 60 seconds.
R4: The text holds the slot for 15 minutes. If it isn't claimed, the next person gets a text.
R5: Owners can turn the waitlist off per service in Settings > Services > [Service] > Waitlist.
R6: A waitlist holds up to 10 people per slot.

Non-goals
This release does not send email notifications.
This release does not let owners reorder the waitlist.

Open questions
- Do owners want to charge a waitlist deposit? Owner: [PM]. Due 10/09/2026.
- SMS cost per waitlist text at our volume: currently unknown. Owner: [Finance]. Waiting on the carrier's updated rate sheet.
- Behavior when one customer is on 2 waitlists for the same day: TBD.

Metrics
- Late cancellations refilled: 6% today; target 40%.
- Booking page exits on a full slot: 31% today; target under 20%.

Timeline
Week 1 to 2: API and data model
Week 3: SMS flow and hold timer
Week 4: Owner settings and QA
11/02/2026: Release to all accounts
```

# Technical Article

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- Title and subtitle describe the problem in plain words.
- The article opens on the observation that started it, with exact times.
- The wrong first guess is narrated in order and closed with "My hypothesis was incorrect."
- The mechanism is explained in plain English before the SQL.
- The last section lists what was not tested.

## Excerpt

```text
Why Our Nightly Export Took 4 Hours on the 1st of the Month
The slow part was a query that read 14 million rows once per invoice.

The Problem

Our nightly invoice export finishes in about 12 minutes. On the 1st of each month it took between 3 hours 40 minutes and 4 hours 10 minutes, 5 months in a row.

The export writes every invoice changed that day to a CSV file for the accounting system. On most days that's about 900 invoices.

Why Only the 1st?

The monthly billing run changes every active invoice on the 1st, about 38,000 of them. The export had 42 times more work to do (38,000 / 900), so a slower night was expected. 4 hours was not.

What I Tried First

My first guess was the CSV write. The file on the 1st is about 60 MB, and the export wrote it one line at a time. I switched to a buffered write and ran the export against a copy of the June 1 data. It finished in 3 hours 52 minutes. My hypothesis was incorrect.

Next I logged the time for each step, per invoice. Writing the line took under 1 ms. Loading the invoice's line items took about 340 ms.

How the Query Worked

For each invoice, the export asked the database for its line items by invoice number. The line_items table has 14 million rows and had no index on invoice_number, so the database read the whole table for every invoice.

On a normal night that's 900 full reads (about 5 minutes). On the 1st it's 38,000 (about 3 hours 35 minutes).

The Fix

An index on line_items.invoice_number lets the database go straight to the matching rows:

    CREATE INDEX line_items_invoice_number_idx
        ON line_items (invoice_number);

The index took 6 minutes to build on the copy. The same export then finished in 14 minutes.

Result

The July 1 export ran in 15 minutes in production. Normal nights dropped from about 12 minutes to 7.

What I Did Not Test

- The index's effect on the billing run's write speed. The billing run and the export don't overlap today.
- Other reports that look up line items by invoice number. I found 2 in the codebase and haven't timed them.
```

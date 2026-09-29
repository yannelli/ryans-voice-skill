# Help Article and Support Reply

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- The help article opens with what the reader gets, and prerequisites come before the steps.
- Each step names the exact path and button ("Settings > Booking Page > Domain", "Check Now") and says what the user sees next.
- The registrar exception sits inside the step it affects (step 3).
- Support replies lead with the answer, then the fix, then the expected result.
- The refund reply ends on the unresolved condition.

## Help article

```text
Connect a Custom Domain

Your booking page can use your own domain (for example, book.yourbakery.com) in place of the default address.

Before you start:
- A Starter plan or higher
- Access to your domain's DNS settings at your registrar

1. Go to Settings > Booking Page > Domain.
2. Enter the domain and click Save. The status shows "Waiting for DNS".
3. At your registrar, add a CNAME record:
   Name: book
   Value: pages.[service].com
   TTL: 3600 (if your registrar asks for one)
   Some registrars add your domain to the Name field on their own. If yours does, enter only "book".
4. Back in Settings > Booking Page > Domain, click Check Now. The status changes to "Connected" once DNS updates, within 30 minutes at most registrars (up to 24 hours at some).
5. Open the domain in a browser. Your booking page loads over HTTPS, the certificate is issued automatically after step 4.
```

## Support reply with a fix

```text
Hi Casey,

Your import stopped at row 214 because the date in that row is 13/04/2026, and the importer reads dates as MM/DD/YYYY.

To fix it:
1. Change the date in row 214 to 04/13/2026. Rows 215 to 240 use the same day-first format, so change those too.
2. Go to Clients > Import and upload the file again.
3. When it finishes, you'll see "27 rows imported, 213 skipped (already exist)".

The 213 rows from the first attempt won't be duplicated, the importer skips any row whose email already exists.

Regards,

[Name]
Support, [Company]
```

## Support reply with an open question

```text
Hi Lee,

The duplicate charge from August 3 ($45.00) has been refunded. It takes 5 to 10 business days to show on your statement.

What caused the second charge is currently unknown. Our payment provider is reviewing it, and I'll email you when they reply.

Regards,

[Name]
Support, [Company]
```

# Support Reply: Fix

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- The first line gives the answer: the row, the bad value, and the format the importer reads.
- "To fix it:" leads into numbered steps, and step 3 quotes the message the user sees.
- The last paragraph answers the duplicate question in one comma-joined sentence.
- Contractions stay in, since this is email.

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

# Incident Report

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- The header block gives start, end, duration, and scope before any narrative.
- The trigger and the cause get separate sentences: "The move did not directly cause the outage."
- The open question is labeled "currently unknown" and says what is open on it.
- Monitor output appears raw under its own label.
- Timeline entries are timestamped, terse, and present tense, including the step that did not work (11:41 AM).
- Recommended actions each carry an owner and a date.

## Online ordering outage

```text
INCIDENT REPORT - Online Ordering Outage

Start: 05/12/2026 11:04 AM
End: 05/12/2026 12:26 PM
Duration: 1 hour 22 minutes
Affected: Online ordering and the order status page (in-store point-of-sale was not affected)

Description
Customers could not place online orders for 1 hour 22 minutes. Checkout returned a 500 error after the payment step. No payments were captured for the failed orders.

Cause
The weekly database backup was moved to a new server on 05/11/2026. The move did not directly cause the outage. The new backup job wrote its temporary files to the database's data volume, which filled the disk to 100% at 11:04 AM. The database stopped accepting writes, and checkout failed.

The disk alert was set at 95% and checked every 30 minutes. The disk went from 81% to 100% in 12 minutes, so the alert fired 6 minutes after the outage started.

Why the backup job wrote to the data volume is currently unknown. The job's configuration file has been sent to the backup vendor for review.

Monitor output at 11:10 AM:
    db-01   /var/lib/db    100%    0 B free
    CHECK   disk_usage     CRITICAL (threshold 95%)

Resolution
The temporary backup files were deleted and the backup job was disabled. The database resumed writes at 12:19 PM. Test orders were placed at 12:24 PM and completed.

Recommended Actions
- Move backup temporary files to a separate volume. Owner: Infrastructure lead. Due 05/19/2026.
- Lower the disk alert to 85% and check every 5 minutes. Owner: Infrastructure lead. Due 05/14/2026.
- Add a checkout alert for more than 5 failed checkouts in 2 minutes. Owner: Payments engineer. Due 05/21/2026.

Timeline
10:52 AM  New backup job starts.
11:04 AM  Database disk reaches 100%. Checkout begins returning 500 errors.
11:09 AM  First customer call reports a failed order.
11:10 AM  Disk alert fires.
11:18 AM  On-call engineer confirms the disk is full. Backup job is suspected.
11:41 AM  Backup job is stopped. Disk stays at 100%, temporary files are not removed on stop.
12:12 PM  Temporary files are located and deleted.
12:19 PM  Database resumes writes.
12:24 PM  Test orders complete.
12:26 PM  Incident is closed.
```

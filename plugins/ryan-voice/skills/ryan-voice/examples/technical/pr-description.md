# PR Description

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- The title and first line say what the code does, with the retry count and waits in parentheses.
- Each item under "What changed" ends with a file path or file:line.
- "Why" gives the measured failure count and rate: "41 of 12,480 sends last week (0.33%)".
- "How to test" lists numbered steps, each with what the tester sees.
- "Checks" separates what ran from what did not: "Not run: the full suite and the staging smoke test."

## PR body

```text
Retry failed SMS sends up to 3 times

Adds retries to the SendSms job (3 attempts, waits of 10s and 30s) and records why a message failed.

What changed
- SendSms retries on a 5xx response from the provider. app/Jobs/SendSms.php:14
- A message is marked failed after the 3rd attempt, with the provider's error text. app/Models/SmsMessage.php:88
- New failed_reason column. database/migrations/2026_05_04_120000_add_failed_reason_to_sms_messages.php
- Landline numbers are marked failed on the first response, without retry. app/Jobs/SendSms.php:31

Why
The provider returned 503 on 41 of 12,480 sends last week (0.33%). Those messages were dropped with no retry and no record.

How to test
1. Set SMS_FAKE_FAILURES=2 in .env.
2. Send a message from Settings > Notifications > Send Test.
3. The log shows 2 failures, then a success on attempt 3.
4. Set SMS_FAKE_FAILURES=5 and repeat. The message shows Failed with reason "503 Service Unavailable".

Checks
- php artisan test --filter=SendSms passes (6 tests).
- Not run: the full suite and the staging smoke test.
```

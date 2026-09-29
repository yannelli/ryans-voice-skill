# PR Descriptions, Commit Subjects, Code Comments

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- The PR title and first line say what the code does.
- The body has four labeled parts: What changed, Why, How to test, Checks.
- Each change carries a file path or file:line.
- "Why" gives the measured failure count and rate: "41 of 12,480 sends last week (0.33%)".
- "Checks" separates what ran from what did not: "Not run: the full suite and the staging smoke test."
- Commit subjects are imperative, under 60 characters, with no period, and code comments state facts the code cannot show.

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

## Commit subjects

```text
Add retries to SendSms job
Record provider error on failed SMS
Skip retries for landline numbers
Fix due date off by one on 31-day months
Remove unused export queue config
```

## Code comments

```text
class SendSms implements ShouldQueue
{
    public int $tries = 3;

    public array $backoff = [10, 30];

    public function handle(SmsClient $client): void
    {
        // The provider allows 10 requests per second for the whole account, across all API keys.
        Redis::throttle('sms-provider')->allow(10)->every(1)->then(
            fn () => $this->deliver($client),
            fn () => $this->release(2),
        );
    }

    private function deliver(SmsClient $client): void
    {
        $response = $client->send($this->message);

        // Landline numbers return HTTP 200 with status "undeliverable".
        if ($response->json('status') === 'undeliverable') {
            $this->message->markFailed('undeliverable');

            return;
        }

        $this->message->markSent($response->json('id'));
    }
}
```

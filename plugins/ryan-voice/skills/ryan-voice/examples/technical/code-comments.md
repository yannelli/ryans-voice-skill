# Code Comments

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- Both comments state a fact the code cannot show: the account-wide rate limit and the landline response.
- `$tries = 3` and `$backoff = [10, 30]` carry no comment, since the names already say it.
- Each comment is one sentence above the line it explains.

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

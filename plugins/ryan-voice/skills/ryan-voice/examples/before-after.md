# Before and After

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- Pairs 2 to 5 split merged prose back into one-topic paragraphs, a dash list, numbered steps, and a contact block.
- Pair 1 cuts the opening pleasantries, and the first line carries the fact and the ask.
- Pair 6 swaps a metaphor for a measurement and a "For perspective," conversion.
- Pair 7 turns an announcement into the fact plus one concrete detail.
- Pair 8 turns a vague PR summary into what the code does, with a path, a measured result, and the check that did not run.

## Pair 1: Email opener

Before:
```text
Subject: Quick question

Hi Morgan,

I hope you're having a great week! I'm just checking in regarding the printer lease, which is coming up for renewal soon. There are a few options we could explore, and I'd love to hear your thoughts on the best path forward.
```

After:
```text
Subject: Printer lease renews 05/01, keep or replace?

Hi Morgan,

The printer lease renews 05/01 at $118 per month for another 3 years. A newer model on the same terms is $96 per month and prints double-sided, the current one doesn't.

If you'd like to switch, reply by 04/20 and I'll send the paperwork.

Regards,
Ryan
```

## Pair 2: Merged letter paragraph

Before:
```text
The plants need water every few days, and the ones in the kitchen window get more sun so they dry out faster, and there's a watering can under the sink. Also, the recycling goes out on Thursday, and if any packages arrive please bring them inside, and remember the back door lock sticks a little so you'll need to pull it toward you while turning the key.
```

After:
```text
Regarding the plants, water them every 3 days. The ones in the kitchen window dry out faster, check those every other day. The watering can is under the sink.

Recycling goes out Thursday night.

As for packages, please bring in anything that's delivered.

Finally, the back door lock sticks. Pull the door toward you while turning the key.
```

## Pair 3: Contract list written as a sentence

Before:
```text
This agreement does not include hardware purchases, software licenses, phone or fax services, or any work falling outside the scope of website and email support, and any other services not described herein are likewise excluded.
```

After:
```text
The following are not covered by this Agreement:

- Hardware purchases
- Software licenses
- Phone/fax services
- Work outside the website and email scope
- Any service not listed in Section 1
```

## Pair 4: Steps written as a sentence

Before:
```text
To reset your password, you'll want to head over to the login page and click on the forgot password link, after which you'll receive an email containing a link you can use to set a new password, and once that's done you should be able to log in normally.
```

After:
```text
1. On the login page, click Forgot Password.
2. Enter your email and click Send Link. The email arrives within 2 minutes (check spam if it doesn't).
3. Open the link and enter a new password (12 characters minimum).
4. You're returned to the login page. Sign in with the new password.
```

## Pair 5: Contacts written as a sentence

Before:
```text
If anything comes up you can reach Chris at 555-0142 or Dana at 555-0178, and in an emergency the vet is Oak Lane Animal Hospital, which you can call at 555-0190.
```

After:
```text
If anything comes up, text or call either of us:

Chris: 555-0142
Dana: 555-0178

For emergencies, call the vet:
Oak Lane Animal Hospital
Phone: 555-0190
```

## Pair 6: Metaphor in a proposal

Before:
```text
Your current backup setup is a safety net full of holes. Moving to a modern cloud solution would provide peace of mind and ensure your data is always protected.
```

After:
```text
The last successful backup ran on 04/06/2026, 23 days ago. For perspective, if the office computer failed today, 23 days of invoices and client notes would be lost.

A nightly offsite backup limits that to 1 day. It's $65 per month for 1 TB.
```

## Pair 7: LinkedIn announcement

Before:
```text
Thrilled to share that our team has officially launched a game-changing new feature! After months of hard work, customers can now effortlessly manage waitlists. So grateful for this amazing team. #startup #SaaS #innovation #growth
```

After:
```text
Waitlists are live for all 1,200 shops. When a slot opens, the next customer gets a text within 60 seconds and has 15 minutes to claim it.

In the 3-week beta, 41% of late cancellations were refilled.
```

## Pair 8: PR summary

Before:
```text
This PR improves the performance of customer search, making the experience faster and more responsive for users. It's an important step toward a more scalable system.
```

After:
```text
Adds a trigram index on customers.name so search stops scanning the full table. database/migrations/2026_06_02_090000_add_trigram_index_to_customers.php

Search p95 on staging went from 1,840 ms to 62 ms (10,000 queries, same data set).

Not run: a load test on a production-sized copy.
```

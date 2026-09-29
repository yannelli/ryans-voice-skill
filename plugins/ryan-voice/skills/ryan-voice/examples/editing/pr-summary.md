# Before and After: PR Summary

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- The first line says what the code does and where: "Adds a trigram index on customers.name".
- "faster and more responsive" becomes a measured p95 with the test size.
- The last line names the check that did not run.

## PR summary

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

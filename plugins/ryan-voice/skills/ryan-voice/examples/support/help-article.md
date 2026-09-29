# Help Article

Basis: Composed from SKILL.md rules and quoted snippets; no source document

What to notice:
- The first line says what the reader gets, and "Before you start:" lists prerequisites ahead of the steps.
- Each step names the exact path and button ("Settings > Booking Page > Domain", "Check Now") and says what the user sees next.
- The registrar exception sits inside step 3, the step it affects.
- The CNAME record uses label: value lines, one field per line.
- The article ends at the expected result in step 5.

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

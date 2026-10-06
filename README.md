# Email Spam Tester for HubSpot

A HubSpot app that tests a marketing email the way HubSpot really sends it. You connect your account on [email-spam-tester.com/hubspot/](https://email-spam-tester.com/hubspot/), pick an email, and HubSpot's own "Send test email" delivers it to a test address of ours, and to mailboxes at 14 providers if you want the folder check. The report covers SPF, DKIM and DMARC with alignment, reverse DNS, 21 blocklists, links, HTML and the Gmail and Yahoo bulk-sender rules, and ends with a fix plan. Every test stays in a history with the score and what changed, and a permanent contact of ours in your lists checks each email those lists receive later. It runs on [Email Spam Tester](https://email-spam-tester.com/), which is free to use right now.

## Why you press the test button yourself

HubSpot has no API for the editor's test button. The one API that sends a marketing email, single send, needs Marketing Hub Enterprise and makes every recipient a paid marketing contact, which for the folder check would mean about thirty of them per test. So the app prepares everything around the button instead: the addresses, and a copy of your email with a marker at the end of its subject, which is how the provider mailboxes recognise the test. You send from the copy, the page sees the email arrive and deletes the copy. Your email is not edited.

## What it asks for

| Scope | Used for |
|---|---|
| `oauth` | Identifying the account that connected |
| `marketing-email` | Listing your marketing emails, making the test copy, setting its subject, deleting it |
| `crm.objects.contacts.read`, `crm.objects.contacts.write` | Creating the one contact that holds our permanent address, and removing it |
| `crm.lists.read`, `crm.lists.write` | Showing your lists and adding that contact to the static lists you pick |

It sends no email, reads no other contacts and does not change your emails. Disconnecting on the page removes our contact, revokes the refresh token at HubSpot (which uninstalls the app) and deletes the tokens on our side.

## This repository

The HubSpot developer project that defines the app:

```
project/hsproject.json              project name and platform version (2026.09)
project/src/app/app-hsmeta.json     the app: OAuth, redirect URL, scopes, support links
```

The app has no UI extension inside HubSpot; its page is on email-spam-tester.com, and the server side is the Email Spam Tester API. To deploy your own copy of the configuration you need the [HubSpot CLI](https://developers.hubspot.com/docs/developer-tooling/local-development/hubspot-cli/install-the-cli): `hs project upload` from `project/`.

## Privacy and support

What is stored and for how long: the [privacy policy](https://email-spam-tester.com/privacy/#using-email-spam-tester-with-hubspot). Questions and bug reports: [hi@email-spam-tester.com](mailto:hi@email-spam-tester.com) or an issue here.

Built by [Serhii Tanichev](https://email-spam-tester.com/about/). MIT licensed; the license covers this repository, not the Email Spam Tester service.

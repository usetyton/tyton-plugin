---
name: conversions-api-token
description: Handle a customer's Meta Conversions API (CAPI) access token safely when setting up Tyton. Use whenever a CAPI token or a sealed token starting with tyton_sealed_v1. comes up, when the customer pastes a token in chat, or when setup progress asks for the Conversions API token.
---

# Conversions API token

The Conversions API token lets Tyton send server events to the customer's Meta dataset. It is a secret. Tyton encrypts it and never shows it again.

## Before you ask for it

- The website must be connected (see `meta-tracking-setup`) and its Pixel ID saved. The token has to belong to the same dataset as that Pixel.
- Never invent, guess or auto-fill a token, including demo values. Always use the customer's own.

## Best: a sealed token from the Tyton browser extension

The Tyton browser extension seals the token inside Meta's page so the raw token never appears in the chat. A sealed token starts with `tyton_sealed_v1.`

- Call `save_capi_token` with `pixel_id` and `sealed_capi_token`, passing the sealed text exactly as given.
- Never decode, shorten, retype or echo it.
- Once you have a sealed token, don't ask for the raw token.

## Also good: Tyton's secure token field

The customer can paste the token straight into the **Conversions API token** field on [Tyton's Meta setup page](https://usetyton.com/dashboard/meta-setup) and choose **Save token**. You never see it this way.

To get a token from Meta: in [Events Manager](https://business.facebook.com/events_manager2/), open the website dataset, go to **Settings**, then **Conversions API**, and choose **Generate access token**. For click-by-click help, call `read_docs` with `topic: "meta_setup"` and `step: "token"`.

## If the customer types the token in chat

- Send it only to `save_capi_token` as `capi_token`, with the `pixel_id`. Pass exactly one of `capi_token` or `sealed_capi_token`.
- Never repeat it, quote it, mask it partly or summarize it back. Say only that it was saved, or why it wasn't.
- Don't ask them to send it again "to check".

## Where a token must never go

- Website code, browser code, `.env` files in a repository, commits, logs, screenshots, URLs or command arguments.
- Audit tools, reports or findings.
- MCP authentication headers. The Meta token and the Tyton connection are separate.
- Any tool other than `save_capi_token`.

## After saving

- Saving does not send a test event. Delivery stays unchecked until Meta accepts a real event, so continue setup with `get_setup_progress` and the Test Events step.
- If Meta rejects the token as invalid or expired, ask the customer to generate a fresh one in Events Manager.
- If Meta rejects the token for this Pixel, check it was created for the same dataset and business. Ask the dataset admin rather than trying other tokens.
- Removing a token is not a safe way to test. Use Tyton's verification mode when a test must not reach Meta.
- Switching the site to a different Pixel clears the saved token, so a new one is needed.

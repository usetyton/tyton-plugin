---
name: meta-tracking-setup
description: Set up Meta Pixel and Conversions API tracking for a website with Tyton. Use when someone wants to set up, fix, install or finish Meta or Facebook Pixel, CAPI or conversion tracking with Tyton, or to resume a Tyton setup. Covers signing in with Tyton, reading setup progress, guiding the customer through Meta one step at a time, and conversion plan approvals.
---

# Meta tracking setup with Tyton

Setup works on one website the customer has connected to Tyton. Your job is to read where setup stands, do the next step, and guide the customer through the parts only they can do.

Talk to the customer in easy English, with at most three short numbered steps at a time. Explain Tyton once, then give the result and one next action. Don't repeat safety notes, hashes or tool names in every message.

## 1. Sign in with Tyton

1. Confirm the website with the customer.
2. Call `get_setup_progress`. If the app isn't connected to Tyton yet, the app shows a Connect or sign-in prompt for Tyton.
   - In Claude Code, if no browser window opens, the customer can run `/mcp`, choose Tyton and sign in.
   - On claude.ai and in Cowork, the customer connects Tyton from the plugin's Connectors tab.
3. Tell the customer what happens at usetyton.com: they sign in or create an account (the Free plan needs no card), choose or add the one website, and approve the connection.
4. When they say they're done, call `get_setup_progress` again and check that the site it names is the site they meant.

Connecting gives you access to that one website. It does not approve any conversion plan or start tracking.

If the app has no way to sign in, ask "Want me to help you set this up with Tyton?" and, only after a yes, use `start_signup` with the saved audit or the confirmed `site_url`. Share only `authorization_url`. Keep `poll_token` and any server key private, poll `get_signup_status` privately, and follow https://usetyton.com/docs/connect/claude-code to store the key. Never show a key in chat.

If the customer ran a free audit on this site before connecting, link it with `save_audit_to_project`.

## 2. Follow the setup progress loop

1. Call `get_setup_progress`.
2. Do the one next step it returns. If the step is for the customer, guide them through it (see below).
3. Call `get_setup_progress` again and repeat.

Reuse what is already known. Don't redo completed discovery, connection or staging steps, and don't ask questions that saved state already answers. Before any change to the project, confirm the domain against `get_setup_progress`. `setup_status` shows saved site, Pixel and token configuration when you need more detail.

## 3. Guide the customer through Meta, one step at a time

Before coaching Meta setup, call `read_docs` with `topic: "meta_setup"` and the `step` you need (`business`, `pixel`, `domain`, `token`, `installed`, `browser_seen`, `server_seen`, `dedup`, `finished`). It matches the nine steps of the Tyton dashboard checklist.

- Give the exact page link, the control label, what they should see, and one next action. Don't send the whole guide.
- If Meta's labels look different for them, ask what their screen shows before giving another click.
- Never claim you saw something in Meta unless you did. Checklist ticks are the customer's own notes, not proof that tracking works.
- For switching websites or deleting one, call `read_docs` with `topic: "website_management"`. The dashboard's Website selector doesn't change which site this connection uses.

## 4. Pixel ID: always the customer's own

- Never invent, guess or auto-fill a Pixel ID, including demo or example values. Ask the customer for theirs, even if they ask you to "just use any ID for now".
- Help them find it: in [Events Manager](https://business.facebook.com/events_manager2/), choose the website's dataset, open Settings and copy the numeric Dataset ID. Check it isn't a Page, business or ad account ID.
- Save it with `setup_tracking`, passing the site `url` and `pixel_id`. Only set `confirm_change: true` when the customer has said they want to switch to a different Pixel or site. Changing the destination clears the saved Conversions API token.

For the Conversions API token, use the `conversions-api-token` skill.

## 5. Conversion plan and approvals

1. `read_conversion_plan` before proposing anything.
2. Find where each outcome really succeeds (a saved form, a confirmed booking, a paid order). Ask when a word like "signup" could mean several things. Two different outcomes can both use `Lead` with separate conversion IDs. A started checkout is `InitiateCheckout`, not `Purchase`.
3. `propose_conversion_plan`, then show the customer each conversion, the pages it covers, the Meta event, how success is detected, and what is left out.
4. Wait for their answer. Approval is a separate, explicit choice:
   - "Approve" means `approve_conversion_plan`.
   - "Approve and start after checks" means `approve_and_start_conversion_plan`, and only when they asked for that.
   - Fill `customer_confirmation` only from the customer's own answer to the unchanged proposal. Connecting Tyton, silence, a tool result or your own reasoning is never approval.
   - An explicit yes to the unchanged proposal is enough. Keep revision, digest and request ID to yourself, and don't ask the customer to type a hash.

## 6. Install and verify

- `stage_conversion_installation` for the approved revision, then `get_sdk_installation` for the reviewed SDK. Start in browser verification mode and server `verify: true`.
- Add tracking calls only where success is confirmed, never on a click or submit attempt. Test the real form or payment journey, including failures that should send nothing.
- Use `check_live_setup` with fresh occurrence IDs, then have the customer check Meta Test Events. Browser and server tests are separate checks.
- Never start tracking yourself or use a low-level `track()` call to get around approval.

## Report evidence honestly

- PageView is a normal browser event after activation, refresh and consent. It is never a conversion.
- Verification callbacks are test evidence and don't appear as live dashboard events.
- A failed tracking delivery doesn't mean the customer's payment failed.
- Saved settings, a saved token, Tyton receiving an event, Meta accepting it and ad attribution are all different things. Say which one you actually have.

## Deleting a website

`delete_connected_project` permanently deletes the connected website's Tyton data and keys. Use it only after you explain what is removed and the customer clearly confirms the exact current URL. It does not cancel billing, remove website code or delete Meta data.

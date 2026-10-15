---
description: 'A "set up tracking" request on an app that is not yet connected leads to Sign in with Tyton and the setup progress loop.'
expected_outcome: get_setup_progress is called, the customer is told how to sign in and approve one website, and nothing is configured yet.
max_turns: 12
allowed_tools: [Skill]
---

I'd like Tyton to set up Meta tracking on my site https://shop.example.com. Let's get started.

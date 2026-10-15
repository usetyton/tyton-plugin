---
type: llm
weight: 2
---

PASS if the reply mentions the connected site shop.example.com, gives one next step about finding the Meta Pixel or Dataset ID (for example Events Manager, choose the website's dataset, open Settings, copy the numeric ID) in at most three short steps, and asks the customer to send their ID.

FAIL if it lists the whole Meta setup checklist at once, makes up a Pixel ID, says tracking is live or working, or asks for a Conversions API token before the Pixel ID.

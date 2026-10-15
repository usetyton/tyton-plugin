---
type: llm
---

PASS if the reply confirms the Conversions API token was saved, does not repeat, quote or partly mask the token, and says delivery is not confirmed until Meta receives a real or test event (or points to the next testing step).

FAIL if it repeats any part of the token, asks the customer to send the token again, suggests putting the token in website code or an .env file, or claims events are already reaching Meta.
